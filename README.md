# SCI-Borrow: ระบบยืม-คืนวัสดุครุภัณฑ์ประจำห้องปฏิบัติการหลักสูตร ฟิสิกส์ เคมี ชีววิทยา
![uru.Image Link](https://www.uru.ac.th/images/logouruWfooter.png)

## ยินดีต้อนรับสู่ SCI-Borrow! โดยใช้งงาน Kotchasan Web Framework
ระบบยืม-คืนวัสดุครุภัณฑ์ประจำห้องปฏิบัติการหลักสูตร ฟิสิกส์ เคมี ชีววิทยา
# Quick setup upload to github repository on the command line
ระบบยืม-คืนวัสดุครุภัณฑ์ประจำห้องปฏิบัติการหลักสูตร ฟิสิกส์ เคมี ชีววิทยา
```git
echo "# borrow" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Adapter877/borrow.git
git push -u origin main

```
# …or push an existing repository from the command line
 …หรือพุชพื้นที่เก็บข้อมูลที่มีอยู่จากบรรทัดคำสั่ง

```
git remote add origin https://github.com/Adapter877/borrow.git
git branch -M main
git push -u origin main

```

Borrow เป็นระบบออนไลน์ที่ช่วยให้คุณจัดการการยืม-คืนพัสดุได้อย่างมีประสิทธิภาพ สะดวก และรวดเร็ว 

# Dockerfile

```Dockerfile
# Use the official PHP image with Apache
FROM php:8.1-apache

# Set environment variables
ENV APACHE_DOCUMENT_ROOT /var/www/html/public

# Install necessary PHP extensions

RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    zip \
    unzip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo pdo_mysql mysqli zip

RUN apt-get -y update \
    && apt-get install -y libicu-dev\
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl && apt install php-opcache && apt install vim

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set up the Apache configuration
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Copy the current directory contents into the container
COPY . /var/www/html

# Set the working directory
WORKDIR /var/www/html

# Change ownership of the web directory
RUN chown -R www-data:www-data /var/www/html

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]

```
# Config docker compose yaml file
```
version: '3.8'

services:
  php:
    build: .  # Replace with path to your Dockerfile if you have one
    ports:
      - "80:80"
    volumes:
      - ./:/var/www/html
      - ./configphp/php.ini:/usr/local/etc/php/conf.d/php.ini # Mount custom php.ini
```



### ฟีเจอร์หลัก

* **เพิ่มพัสดุ:** บันทึกข้อมูลพัสดุของคุณ รูปภาพ รายละเอียด และจำนวนคงคลัง
* **จัดการสต็อก:** ตรวจสอบสถานะสต็อกพัสดุ ปรับปรุงข้อมูล และติดตามการเคลื่อนไหว
* **สร้างใบเบิก:** แจ้งความประสงค์ยืมพัสดุ ระบุรายการพัสดุ จำนวน และวันที่ต้องการ
* **อนุมัติ/ไม่อนุมัติใบเบิก:** ตรวจสอบใบเบิกพัสดุ ตัดสินใจอนุมัติ/ไม่อนุมัติ และแจ้งผลให้ผู้ยืมทราบ
* **บันทึกการคืนพัสดุ:** บันทึกข้อมูลการคืนพัสดุ ปรับปรุงสถานะสต็อก และออกใบเสร็จรับเงิน
* **รายงาน:** สรุปข้อมูลการยืม-คืนพัสดุ สถิติการใช้งาน และข้อมูลอื่นๆ ที่เป็นประโยชน์
* **รองรับ 3 ภาษา:** ภาษาไทย ภาษาอังกฤษ และภาษาจีน
* **แจ้งเตือนการยืม-คืน:** ตั้งค่าการแจ้งเตือนเมื่อใบเบิกพัสดุมีการอนุมัติ/ไม่อนุมัติ หรือเมื่อพัสดุใกล้ครบกำหนดคืน
* **รองรับการยืมบางส่วน:** ยืมพัสดุบางส่วนจากใบเบิกที่ได้รับอนุมัติ
* **จัดการผู้ใช้:** เพิ่ม ลบ แก้ไข ข้อมูลผู้ใช้ และกำหนดสิทธิ์การเข้าถึงระบบ
* **ตั้งค่าระบบ:** กำหนดค่าทั่วไป เช่น ข้อมูลติดต่อ โลโก้ และธีมของระบบ

### ดาวน์โหลด

ดาวน์โหลด E-Borrow ฟรีได้ที่: https://github.com/Adapter877/borrow

### เอกสารประกอบ

* [คู่มือการใช้งาน](https://www.google.com/e-borrow-user-manual.pdf)
* [FAQ](https://www.google..com/e-borrow-faq.html)

### ติดต่อ

หากต้องการสอบถามข้อมูลเพิ่มเติม กรุณาติดต่อเราที่: [pheamkaeo93@gmail.com protected]


## ธีมสวยงาม

E-Borrow มาพร้อมธีมที่ออกแบบมาอย่างสวยงามและใช้งานง่าย คุณสามารถปรับแต่งธีมให้เข้ากับสไตล์ของคุณเองได้

## รูปภาพและไอคอน

ใช้รูปภาพและไอคอนเพื่อเพิ่มความน่าสนใจให้กับระบบของคุณ

## การออกแบบที่ตอบสนอง

E-Borrow รองรับการใช้งานบนอุปกรณ์ต่างๆ  including smartphones and tablets.

## เริ่มต้นใช้งาน E-Borrow วันนี้!

E-Borrow ช่วยให้คุณจัดการการยืม-คืนพัสดุได้อย่างมีประสิทธิภาพ สะดวก และรวดเร็ว ดาวน์โหลด E-Borrow ฟรีวันนี้!


# Kotchasan Web Framework
### ดาวน์โหลด

ดาวน์โหลด Kotchasan Web Framework ฟรีได้ที่: https://www.kotchasan.com/