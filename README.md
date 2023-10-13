@Test
    public void testGetIconIDForSnow() {
        // Test for "snow" condition
        int condition = 610;  // A value within the range 600-622
        long sunrise = 1600;  // sunrise time
        long update_time = sunrise + 1500;  // A time during the day
        long sunset = 1700;  // sunset time

        String iconID = getIconID(condition, update_time, sunrise, sunset);

        assertEquals("snow", iconID);
}

<h3> ชื่อของ test case: testGetIconIDForSnow</h3>

**จุดประสงค์ของ test case นี้เพื่อทดสอบฟังก์ชัน getIconID ในกรณีของ condition ที่เป็น "snow" โดยกำหนดค่า condition เป็น 610 และตรวจสอบว่าเมื่อเรียกใช้ getIconID และค่าที่คืนค่าคือ "snow" ตามที่คาดหวังหรือไม่**

**interface-based characteristics** 
1. Identify testable functions: 'testGetIconIDForSnow()'
2. Identify parameters, return types, return values, and exceptional behavior
   - Parameters: condition (int), update_time, sunrise, sunset
   - Return type: String
   - Return value: ค่า String ของ icon ที่สอดคล้องกับเงื่อนไขสภาพอากาศที่กำหนด
3. Model the input domain
   - C1 = 'condition' = 600-622
   - C2 = 'update_time' = A long integer representing the time of the weather update.(ต้องเป็นเวลาหลังจาก sunrise และก่อน sunset)
   - C3 = 'sunrise'= A long integer representing the time of sunrise.
   - C4 = 'sunset' = A long integer representing the time of sunset.

**Partition Characteristics**

|  Characteristics             |  B1  |  B2   |
|-------------------------------------------------|------|-------|
| C1 = 'condition' = 600-622                      | True | False |
|-------------------------------------------------|------|-------|
| C2 = 'update_time' is time of the weather update| True | False |
|-------------------------------------------------|------|-------|
| C3 = 'sunrise' is time of sunrise               | True | False |
|-------------------------------------------------|------|-------|
| C4 = 'sunset' is time of sunset                 | True | False |


**Identify Values**

|  Characteristics             |  B1  |  B2   |
|-------------------------------------------------|------|-------|
| C1 = 'condition' = 600-622                      | 610 | 650 |
|-------------------------------------------------|------|-------|
| C2 = 'update_time' is time of the weather update| 1600 | 1500 |
|-------------------------------------------------|------|-------|
| C3 = 'sunrise' is time of sunrise               | 1600 | 1700 |
|-------------------------------------------------|------|-------|
| C4 = 'sunset' is time of sunset                 | 1700 | 1600 |

**การรวม partition  โดยใช้วิธีการ ECC**

|  Characteristics  | B1  | B2 |
|--------|------------|----------|
|  C1    |  A     |   B   |
|--------|------------|----------|
|  C2    |  C      |   D   |
|--------|------------|----------|
|  C3    |  X      |   Y   |
|--------|------------|----------|
|  C4    |  1      |   2   |

Test Requirements = 2
(A, C, X, 1), (B, D, Y, 2)

**Functionality-based Characteristics**
1. Identify testable functions: 'testGetIconIDForSnow()'
2. Identify parameters, return types, return values, and exceptional behavior
   - Parameters: condition (int), update_time, sunrise, sunset
   - Return type: String
   - Return value: ค่า String ของ icon ที่สอดคล้องกับเงื่อนไขสภาพอากาศที่กำหนด
3. Model the input domain
   - C1 = 'condition' Positive Test Case: 610, Negative Test Case: 650
   - C2 = 'update_time' = Positive Test Case: sunrise + 1000, Negative Test Case: sunrise - 1000
   - C3 = 'sunrise'= Positive Test Case: 1600, Negative Test Case: 1500 or 1700
   - C4 = 'sunset' = Positive Test Case: 1700, Negative Test Case: 1500 or 1600

**Partition Characteristics**

|  Characteristics             |  B1  |  B2   |    B3    |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 600-622                      | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| True | False | False |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | True | False | False |

**Identify Values**

|  Characteristics             |  B1  |  B2   |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 600-622                      | 610 | 650 |    |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| 1600 | 1600 |  1700 |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | 1600 | 1700 |  |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | 1700 | 1600 |  |

**Derive Test** ECC

|Test	| condition |	update_time	| sunrise	| sunset |	Expected |
|---- |-----------|-------------|---------|------  |-----------|
| T1	| 610	      | 1600	      | 1600	  | 1700	 | Snow
|---- |-----------|-------------|---------|------  |-----------|
| T2	| 610	      | 1600	      | 1700	  | 1600	 | null
|---- |-----------|-------------|---------|------  |-----------|
| T3	| 610	      | 1600	      | 1650	  | 1650	 | Snow
|---- |-----------|-------------|---------|------  |-----------|
| T4	| 650	      | 1600	      | 1600	  | 1700	 | null
|---- |-----------|-------------|---------|------  |-----------|
| T5	| 625	      | 1700	      | 1700	  | 1600	 | null

 


@Test
    public void testGetIconIDForWind() {
        // Test for "wind" condition
        int condition = 701;  // A value within the range 701-781
        long update_time = 0;  // We don't need to consider update_time for "wind"
        long sunrise = 1600;  // Example sunrise time
        long sunset = 1700;  // Example sunset time

        String iconID = getIconID(condition, update_time, sunrise, sunset);

        assertEquals("wind", iconID);
}

<h3> ชื่อของ test case: testGetIconIDForWind</h3>

**จุดประสงค์ของ test case นี้เพื่อทดสอบฟังก์ชัน getIconID ในกรณีของ condition ที่เป็น "wind" โดยกำหนดค่า condition เป็น 610 และตรวจสอบว่าเมื่อเรียกใช้ getIconID และค่าที่คืนค่าคือ "wind" ตามที่คาดหวังหรือไม่**

**interface-based characteristics** 
1. Identify testable functions: 'testGetIconIDForWind()'
2. Identify parameters, return types, return values, and exceptional behavior
   - Parameters: condition (int), update_time, sunrise, sunset
   - Return type: String
   - Return value: ค่า String ของ icon ที่สอดคล้องกับเงื่อนไขสภาพอากาศที่กำหนด
3. Model the input domain
   - C1 = 'condition' = 701-781
   - C2 = 'update_time' = A long integer representing the time of the weather update.(ต้องเป็นเวลาหลังจาก sunrise และก่อน sunset)
   - C3 = 'sunrise'= A long integer representing the time of sunrise.
   - C4 = 'sunset' = A long integer representing the time of sunset.

**Partition Characteristics**

|  Characteristics             |  B1  |  B2   |    B3    |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 701-781                      | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| True | False | False |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | True | False | False |


**Identify Values**

|  Characteristics             |  B1  |  B2   |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 600-622                      | 701 | 790 |  785  |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| 0 | 0 |  1700 |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | 1600 | 1700 | 1650 |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | 1700 | 1600 | 1650 |

**การรวม partition  โดยใช้วิธีการ ECC**

|  Characteristics  | B1  | B2 |  B3  |
|--------|------------|----------------|
|  C1    |  A     |   B   |   E    |
|--------|------------|----------|
|  C2    |  C      |   D   |   F   |
|--------|------------|----------|
|  C3    |  X      |   Y   |   G    |
|--------|------------|----------|
|  C4    |  1      |   2   |   3   |

Test Requirements = 3
(A, C, X, 1), (B, D, Y, 2), (E, F, G, 3)

**Functionality-based Characteristics**
1. Identify testable functions: 'testGetIconIDForWind()'
2. Identify parameters, return types, return values, and exceptional behavior
   - Parameters: condition (int), update_time, sunrise, sunset
   - Return type: String
   - Return value: ค่า String ของ icon ที่สอดคล้องกับเงื่อนไขสภาพอากาศที่กำหนด
3. Model the input domain
   - C1 = 'condition' Positive Test Case: 701, Negative Test Case: 790
   - C2 = 'update_time' = Positive Test Case: 0, Negative Test Case: ไม่มีข้อจำกัดในเวลา
   - C3 = 'sunrise'= Positive Test Case: 1600, Negative Test Case: 1500 or 1700
   - C4 = 'sunset' = Positive Test Case: 1700, Negative Test Case: 1500 or 1600

**Partition Characteristics**

|  Characteristics             |  B1  |  B2   |    B3    |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 701-781                      | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| True | False | False |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | True | False | False |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | True | False | False |

**Identify Values**

|  Characteristics             |  B1  |  B2   |
|-------------------------------------------------|------|-------|-------|
| C1 = 'condition' = 600-622                      | 701 | 790 |  785  |
|-------------------------------------------------|------|-------|-------|
| C2 = 'update_time' is time of the weather update| 0 | 0 |  1700 |
|-------------------------------------------------|------|-------|-------|
| C3 = 'sunrise' is time of sunrise               | 1600 | 1700 | 1650 |
|-------------------------------------------------|------|-------|-------|
| C4 = 'sunset' is time of sunset                 | 1700 | 1600 | 1650 |

**Derive Test** 

|Test	| condition |	update_time	| sunrise	| sunset |	Expected |
|---- |-----------|-------------|---------|------  |-----------|
| T1	| 701	      | 0	          | 1600	  | 1700	 | Wind
|---- |-----------|-------------|---------|------  |-----------|
| T2	| 781	      | 0	          | 1600	  | 1700	 | Wind
|---- |-----------|-------------|---------|------  |-----------|
| T3	| 701	      | 0	          | 1700	  | 1600	 | null
|---- |-----------|-------------|---------|------  |-----------|
| T4	| 701	      | 0	          | 1650	  | 1650	 | Wind
|---- |-----------|-------------|---------|------  |-----------|
| T5	| 790	      | 0	          | 1600	  | 1700	 | null

 
