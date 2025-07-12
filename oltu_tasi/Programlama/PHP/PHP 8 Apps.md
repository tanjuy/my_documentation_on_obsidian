### Uygulama 1:

**connect_postgresql.php:**

```php
<?php
try {
    /*
    $con_psql = new PDO (
        "pgsql:host=192.168.1.132;
        port=5432;
        dbname=pdo_tutorial;
        user=tanju;
        password=1234tyod"
    );
    */

    // Alternatif Bağlantı:
    $db_name = "pgsql:host=192.168.1.132; port=5432; dbname=pdo_tutorial";
    $con_psql = new PDO ($db_name, 'tanju', "1234tyod");


    $con_psql->setAttribute(
        PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC
    );

    echo "Connection is successful\n";

} catch (PDOexception $e) {
    echo "Connection is failed!";
    echo "Bağlantı Hatası:" . $e->getMessage();
}

?>
```

**app.php:**

```php
<?php
// Uygulama 3:

include 'connect_postgres1.php';

function &input($info) {
    $data = mb_convert_case(
        mb_strtolower(readline($info),'UTF-8'),
        MB_CASE_TITLE, 'UTF-8'
    );
    return $data;
}


function input_date() {
    while (true) {
        $dob = input('Doğum Tarihiniz(Gün/Ay/Yıl): ');
        $date_format = DateTime::createFromFormat('d/m/Y', $dob);

        $errors = DateTime::getLastErrors();

        if ($date_format === false || $errors['warning_count'] > 0 || $errors['error_count'] > 0) {
            echo "❌ Hatalı format! Lütfen tarihi 'GG/AA/YYYY' şeklinde giriniz. Örn: 12/10/1999\n\n";
            continue;
        }

        $dob_output = $dob;

        $today = new DateTime();
        $birthday = new DateTime($date_format->format('Y-m-d'));
        $age_obj = $today->diff($birthday);

        return [$age_obj->y, $dob_output];
    }
}


for (;;) {
    $input_letter = input(
        "Çıkmak için 'Q', Devam için Enter tuşuna basın: "
    );
    if (strtoupper($input_letter) === 'Q') {
        break;
    }

    $insert_query = $con_psql->prepare(
        'INSERT INTO employee_data (
            emp_name, emp_place, emp_age, emp_dob
        )
        VALUES (
            :emp_name, :emp_place, :emp_age, :emp_dob
        )'
    );


    $name = input('İsim giriniz: ');

    $dizi = input_date();

    $insert_query->execute([
        ':emp_name' => $name,
        ':emp_place' => input('Yer giriniz: '),
        ':emp_age' => $dizi[0],
        ':emp_dob' => $dizi[1]
    ]);

    echo "\nGirilen en son verinin ID: " .
        $con_psql->lastInsertId() . "\n";
}
?>
```