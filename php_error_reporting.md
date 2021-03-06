![](images/day6.png)

# PHP error_reporting()
`error_reporting()` ใช้สำหรับแสดงข้อผิดพลาด (Error) ของโปรแกรม PHP โดยแสดงว่ามีข้อผิดพลาดอะไรเกิดขึ้น เพื่อ Dev สามารถแก้ไขได้ง่ายและถูกจุด สะดวกต่อการทำ Debug ในด้าน Security หากข้อผิดพลาดเกิดไปแสดงต่อผู้ไม่ประสงค์ดีสามารถนำไปสู่การแฮกได้  

### รูปแบบการใช้งาน

```php 
error_reporting ( int $level = ? ) : int
```

### Parameters 

- `level` - สำหรับกำหนด level การรายงานข้อผิดพลาด (Error) สำหรับสคริปต์ปัจจุบัน ค่าที่ยอมรับคือ constant name และ Value number

### ค่าคงที่ที่กำหนดไว้มีดังนี้
1. `E_Error` - ใช้บอกถึง Runtime errors ที่ร้ายแรงที่ไม่สามารถกู้คืนได้และจะหยุดการทำงานของสคริปต์
2. `E_Warning` - ข้อผิดพลาดที่ไม่ร้ายแรงซึ่งสคริปต์สามารถทำงานต่อไปได้
3. `E_Parse` - ข้อผิดพลาดในการวิเคราะห์ compile-time ซึ่งจะถูกสร้างขึ้นโดยตัววิเคราะห์เท่านั้น
4. `E_Notice` - ปัญหานี้แจ้งเกี่ยวกับ Runtime ที่ระบุว่าสคริปต์พบสิ่งที่แสดงข้อผิดพลาด แต่อาจเกิดขึ้นได้ในขณะที่เรียกใช้สคริปต์ปกติ
5. `E_Core_Error` - ในระหว่างการ Start ของ PHP อาจมีข้อผิดพลาดร้ายแรงเกิดขึ้นซึ่งเกิดจาก PHP core
6. `E_Core_Warning` - ข้อผิดพลาดที่ไม่ร้ายแรงซึ่งเกิดขึ้นระหว่างการ  Start ครั้งแรกของ PHP ซึ่งสร้างโดย PHP core
7. `E_Compile_Error` - ข้อผิดพลาดร้ายแรงซึ่งเกิดขึ้นระหว่าง compile-time สิ่งเหล่านี้สร้างขึ้นโดยกลไกการเขียน Zend สคริปต์ 
8. `E_Compile_Warning` - คล้ายกับ `E_Compile_Error` คำเตือน compile-time การแสดงผลเหล่านี้หรือเรียกได้ว่าเป็นข้อผิดพลาดที่ไม่ร้ายแรง  และถูกสร้างโดยเครื่องมือเขียน  Zend สคริปต์
9. `E_User_Error` - ข้อผิดพลาดที่สร้างขึ้นโดยผู้ใช้ คล้ายกับ `E_ERROR` ยกเว้นว่าสร้างขึ้นโดยใช้ฟังก์ชัน PHP ในโค้ด PHP
10. `E_USER_WARNING` - ข้อความเตือนที่ผู้ใช้สร้างขึ้น `E_USER_WARNING` เหมือนกับ `E_WARNING` ยกเว้นว่าสร้างขึ้นในโค้ด PHP โดยใช้ฟังก์ชัน PHP `trigger_error()`
11. `E_USER_NOTICE` - ข้อความแจ้งเตือนที่ผู้ใช้สร้างขึ้น `E_USER_NOTICE` เหมือนกับ `E_NOTICE` ยกเว้นว่าสร้างขึ้นในโค้ด PHP โดยใช้ฟังก์ชัน PHP `trigger_error()`
12. `E_STRICT` -  Enable เพื่อให้ PHP แนะนำว่าแก้ไขโค้ดอย่างไร ซึ่งจะช่วยให้มั่นใจได้ถึงการทำงานร่วมกันที่ดีที่สุด และยังทำให้โค้ดทำงานเข้ากันได้ดีด้วย
13. `E_RECOVERABLE_ERROR` - ข้อผิดพลาดร้ายแรงที่ตรวจจับได้ แสดงว่าอาจมีข้อผิดพลาดที่เป็นอันตรายเกิดขึ้น แต่ไม่ได้ทำให้การทำงานอ่อนลง หากข้อผิดพลาดไม่ถูกตรวจจับโดยจุดที่ตรวจจับนั้นผู้ใช้กำหนดเอง (ดูเพิ่มเติมที่ [set_error_handler()](http://php.adamharvey.name/manual/en/function.set-error-handler.php)) แอปพลิเคชันที่รันจะถูกยกเลิกเนื่องจากเป็น `E_ERROR`
14. `E_DEPRECATED` - แจ้ง Runtime เปิดใช้งาน `E_DEPRECATED` เพื่อแสดงคำเตือนเกี่ยวกับโค้ดที่จะใช้ไม่ได้ในเวอร์ชันอนาคต
15. `E_USER_DEPRECATED` - ข้อความเตือนที่ผู้ใช้สร้างขึ้น `E_USER_DEPRECATED` เหมือนกับ `E_DEPRECATED` ยกเว้นว่าสร้างขึ้นในโค้ด PHP โดยใช้ฟังก์ชัน PHP `trigger_error()`
16. `E_All` - ข้อผิดพลาดนี้เหมือนกับการรวมกันของทั้งหมดข้างต้น ซึ่งรองรับ Error และคำเตือนทั้งหมดยกเว้น `E_STRICT`

### การคืนค่า

จะคืนค่า level ของ`error_reporting` ก่อนหน้า หรือ level ปัจจุบันหากไม่มีการกำหนด level parameter

### ตัวอย่างการใช้ `error_reporting()`

### ตัวอย่างแบบที่ 1 

```php 
<?php

// ปิดทุกรายงานข้อผิดพลาด
error_reporting(0);

// รายงานข้อผิดพลาดในการทำงานง่าย ๆ
error_reporting(E_ERROR | E_WARNING | E_PARSE);

// การรายงาน `E_ NOTICE` สามารถทำได้ดีเช่นเดียวกัน (ในการรายงานแบบไม่เปิดเผย)
// ตัวแปรหรือจับชื่อตัวแปรที่สะกดคำผิด... )
error_reporting(E_ERROR | E_WARNING | E_PARSE | E_NOTICE);

// รายงานข้อผิดพลาดทั้งหมดยกเว้น `E_ NOTICE`
error_reporting(E_ALL & ~E_NOTICE);

// รายงานข้อผิดพลาดทั้งหมดของ PHP (ดู changlog)
error_reporting(E_ALL);

// รายงานข้อผิดพลาดทั้งหมดของ PHP
error_reporting(-1);

// เหมือนกับ `error_reporting(E_ALL);`
ini_set('error_reporting', E_ALL);

?>
```
### ตัวอย่างแบบที่ 2 ใช้จัดการข้อผิดพลาด (Error) ในสคริปต์

```php
<?php
// จัดการข้อผิดพลาดเอง
error_reporting(0);

// ฟังก์ชันการจัดการข้อผิดพลาดที่กำหนดโดยผู้ใช้
function userErrorHandler($errno, $errmsg, $filename, $linenum, $vars) {
    // timestamp สำหรับรายการ Error
    $dt = date("Y-m-d H:i:s (T)");

    // แก้ไขอาร์เรย์ของสตริงที่มีข้อผิดพลาด
    // จริง ๆ แล้วควรทำแค่รายการเดียว
    // มี 2,8,256,512 และ 1024
    $errortype = array (
                1    =>  "Error",
                2    =>  "Warning",
                4    =>  "Parsing Error",
                8    =>  "Notice",
                16   =>  "Core Error",
                32   =>  "Core Warning",
                64   =>  "Compile Error",
                128  =>  "Compile Warning",
                256  =>  "User Error",
                512  =>  "User Warning",
                1024 =>  "User Notice"
                );
    // Set ของ Error
    $user_errors = array(E_USER_ERROR, E_USER_WARNING, E_USER_NOTICE);
    
    $err = "<errorentry>\n";
    $err .= "\t<datetime>" . $dt . "</datetime>\n";
    $err .= "\t<errornum>" . $errno . "</errornum>\n";
    $err .= "\t<errortype>" . $errortype[$errno] . "</errortype>\n";
    $err .= "\t<errormsg>" . $errmsg . "</errormsg>\n";
    $err .= "\t<scriptname>" . $filename . "</scriptname>\n";
    $err .= "\t<scriptlinenum>" . $linenum . "</scriptlinenum>\n";

    if (in_array($errno, $user_errors))
        $err .= "\t<vartrace>" . wddx_serialize_value($vars, "Variables") . "</vartrace>\n";
    $err .= "</errorentry>\n\n";
    
    // for testing
    // echo $err;

    // บันทึกข้อผิดพลาดลงใน error log `error_log()` และให้ส่งอีเมลให้หากมีข้อผิดพลาดร้ายแรงของผู้ใช้
    error_log($err, 3, "/usr/local/php4/error.log");
    if ($errno == E_USER_ERROR)
        mail("phpdev@example.com", "Critical User Error", $err);
}


function distance($vect1, $vect2) {
    if (!is_array($vect1) || !is_array($vect2)) {
        trigger_error("Incorrect parameters, arrays expected", E_USER_ERROR);
        return NULL;
    }

    if (count($vect1) != count($vect2)) {
        trigger_error("Vectors need to be of the same size", E_USER_ERROR);
        return NULL;
    }

    for ($i=0; $i<count($vect1); $i++) {
        $c1 = $vect1[$i]; $c2 = $vect2[$i];
        $d = 0.0;
        if (!is_numeric($c1)) {
            trigger_error("Coordinate $i in vector 1 is not a number, using zero",
                            E_USER_WARNING);
            $c1 = 0.0;
        }
        if (!is_numeric($c2)) {
            trigger_error("Coordinate $i in vector 2 is not a number, using zero",
                            E_USER_WARNING);
            $c2 = 0.0;
        }
        $d += $c2*$c2 - $c1*$c1;
    }
    return sqrt($d);
}

$old_error_handler = set_error_handler("userErrorHandler");

// ค่าคงที่ที่ไม่ได้กำหนด, ให้ generates a warning  
$t = I_AM_NOT_DEFINED;

// กำหนดเวกเตอร์บางส่วน
$a = array(2, 3, "foo");
$b = array(5.5, 4.3, -1.6);
$c = array (1, -3);

// generate a user error
$t1 = distance($c, $b) . "\n";

// generate another user error
$t2 = distance($b, "i am not an array") . "\n";

// generate a warning
$t3 = distance($a, $b) . "\n";

?> 
```


#### Reference
- https://www.php.net/manual/en/function.error-reporting.php
- http://php.adamharvey.name/manual/en/errorfunc.constants.php
- https://www.macs.hw.ac.uk/~hwloidl/docs/PHP/ref.errorfunc.html#e-error

