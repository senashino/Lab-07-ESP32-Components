# Lab 7-1: Local Component Demo

## สรุปคำสั่งที่ใช้ และผลลัพธ์ที่ได้
<1. ตั้งค่า target ESP32 โดยใช้คำสั่ง idf.py set-target esp32 โดย ESP-IDF จะสร้างไฟล์ sdkconfig ใหม่ และตั้งค่า target เป็น ESP32 
    2. แก้ไขไฟล์ CMakeLists.txt ของโปรเจกต์ จากเดิม 
    cmake_minimum_required(VERSION 3.16)
    include($ENV{IDF_PATH}/tools/cmake/project.cmake)
    project(lab7-1)
    เปลี่ยนเป็น 
    cmake_minimum_required(VERSION 3.16)

    # เพิ่มบรรทัดนี้ เพื่อให้ CMake มองหา components ที่อยู่นอก main
    set(EXTRA_COMPONENT_DIRS ../components)

    include($ENV{IDF_PATH}/tools/cmake/project.cmake)
    project(lab7-1)

    ผลลัพธ์: - Compiler จะเจอ sensor.h จาก ../components/Sensors
            - build ผ่าน ไม่มี error fatal error: sensor.h: No such file or directory
            - ได้ไฟล์ .elf, .bin ในโฟลเดอร์ build/ พร้อม flash ลง ESP32
            - ใช้ idf.py fullclean → เคลียร์ build เก่า
            - ใช้ idf.py build → build ใหม่  เจอ sensor.h และ compile ผ่าน
    >
