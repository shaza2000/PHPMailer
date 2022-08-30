<?php


if(isset($_POST['reset'])){
    $email=$_POST['email'];
}
else {
    exit(); 
}

use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

/*
replace this path:
    require 'path/to/PHPMailer/src/Exception.php';
to:
    require 'mail/Exception.php';
*/
require 'mail/Exception.php';
require 'mail/PHPMailer.php';
require 'mail/SMTP.php';

//Create an instance; passing `true` enables exceptions
$mail = new PHPMailer(true);

try {
    //Server settings
    /*remove server debug 
    $mail->SMTPDebug = SMTP::DEBUG_SERVER;                      //Enable verbose debug output
    */
    $mail->isSMTP();                                            //Send using SMTP
    /*
    here change: 
        $mail->Host= 'smtp.example.com';
    to:
        $mail->Host= 'smtp.gmail.com';
    */

    //in note check direction change
    $mail->Host = 'smtp.gmail.com';                             //Set the SMTP server to send through 
    $mail->SMTPAuth = true;                                     //Enable SMTP authentication   
    /*
    here change: 
        $mail->Username   = 'user@example.com';
    to:
        $mail->Username   = 'example@gmail.com';
    */
    $mail->Username   = 'example@gmail.com';   //SMTP username
    /*
    here change: 
        $mail->Password   = 'secret';
    to in phpmyadmin password this email password is a:
        $mail->Password   = 'a';
    */
    $mail->Password   = '*****';                            //SMTP password
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;     //Enable implicit TLS encryption or 'tls'; 
    $mail->Port       =587;                            // TCP port to connect to, use 465 for  `PHPMailer::ENCRYPTION_SMTPS` above 

    /*Have two option port:
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
    $mail->Host = 'smtp.gmail.com';
    $mail->Port = 587;

    or 
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_SMTPS;
    $mail->Host = 'smtp.gmail.com';
    $mail->Port = 465;
    */

    //Recipients
     /*
    here change: 
        $mail->setFrom('from@example.com', 'Mailer');
    to:
        $mail->setFrom('example@gmail.com', 'Mailer');
    */
    $mail->setFrom('example@gmail.com', 'Admin');
    /*
    here change: 
        $mail->addAddress('joe@example.net', 'Joe User'); 
    to:
        $mail->addAddress($email); 
    */
    $mail->addAddress($email);                              //Add a recipient
    /*Comment this option

    $mail->addAddress('ellen@example.com');               //Name is optional
    $mail->addReplyTo('info@example.com', 'Information');
    $mail->addCC('cc@example.com');
    $mail->addBCC('bcc@example.com');
    
    //Attachments
    $mail->addAttachment('/var/tmp/file.tar.gz');         //Add attachments
    $mail->addAttachment('/tmp/image.jpg', 'new.jpg');    //Optional name
    */

    //ADD THIS $code
    $code = substr(str_shuffle('1234567890WERTYUIOPASDFGHJKLZXCVBNM'),0,10); //This function shows random numbers and letters when I change the password and it appears in the URL of this page and also in the DB

    //Content
    $mail->isHTML(true);                                  //Set email format to HTML
    /*here change:
        $mail->Subject = 'Here is the subject';
    to:
        $mail->Subject = 'Password Reset';
    */
    $mail->Subject = 'Password Reset';

    /*here change:
        $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    to:
        $mail->Body    = 'To Reset Your Password click <a href="http://localhost/TechnologyInHorseEnvironment/Html/login_system/change_password.php?code='.$code.'">here </a>.</br> Reset Your Password in a Day.';
    */
    $mail->Body    = 'To Reset Your Password click <a href="http://localhost/TechnologyInHorseEnvironment/Html/login_system/change_password.php?code='.$code.'">here </a>.</br> Reset Your Password in a Day.';
    /*Comment this option 
    $mail->AltBody = 'This is the body in plain text for non-HTML mail clients';
    */

    //NOW GO TO GOOGLE GMAIL SECURITY
    //https://myaccount.google.com/security?pli=1
    //in search write Less Security App Access --> Turn on
    //https://myaccount.google.com/lesssecureapps?pli=1&rapt=AEjHL4OaNadjwTHpPyFANJe0aPa9hOli1rdV2_vj3Smq9s6pX-nZtn22NsTKmkaqX8WwPI0Q2mrVPecuv3dilAemYPfPSXX-0Q


    //here connection to DB
    $conn = new mySqli('localhost', 'root', '', 'technologyinhorseenvironment');

    if($conn->connect_error) {
        die('Could not connect to the database.');
    }
    
        
    //verify 
    $verifyQuery = $conn->query("SELECT * FROM ColumName WHERE email = '$email'");

    if($verifyQuery->num_rows) {
        $codeQuery = $conn->query("UPDATE ColumName SET code = '$code' WHERE email = '$email'");
            
        $mail->send();
        echo 'Message has been sent, check your email';
    }
    $conn->close();
    

} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
?>
