# PHP
String manipulation using php

<?php 
if(isset($_POST['string'])){

  $string = $_POST['string'];
  $word_count='';
  $char_count='';
  $vowel_count='';
  $upper_vowel='';

      echo "<b>Input string:</b>";
      echo $string;
      echo "<br>";
    
    
      echo "<b>Word Count:</b>";
      echo $word_count=str_word_count("$string")."<br>";
 
    
      echo "<b>Character Count:</b>";
      echo $char_count = strlen("$string")."<br>";
      
    
      echo "<b>Vowels Count:</b>";
      echo  $vowel_count = preg_match_all('/[aeiou]/i',$string,$matches);
      echo "<br>";

      echo "<b>Vowels in UpperCase:</b>";
      $upper_vowel = str_ireplace(array('a','e','i','o','u',), array('A','E','I','O','U'), $string);
      echo $upper_vowel;
      

       $server = "localhost";
       $username = "root";
       $password = "";
       $dbname = "string_data";
   
       // Create a database connection
      //  $con = mysqli_connect($server, $username, $password);
      $con = new mysqli($server, $username, $password, $dbname);
       // Check for connection success
      if(!$con){
           die("connection to this database failed due to" . mysqli_connect_error());
      }
    //  echo "Success connecting to the db";


        

        $SQL_INSERT = "INSERT INTO data (string, word_count, char_count, vowel_count, upper_vowel) VALUES (?,?,?,?,?)";
        $stmt = $con->prepare($SQL_INSERT);
        // prepare and bind
        if($stmt = $con->prepare($SQL_INSERT)) { 
        $stmt->bind_param("siiis", $string, $word_count, $char_count, $vowel_count, $upper_vowel);
        $stmt->execute();
        //echo "Success connecting to the db";
        }
        else {
        $error = $con->errno . ' ' . $con->error;
        echo $error;
          }
        $con->close();
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Strings Manipulation</title>
    <!-- <link rel="stylesheet" href="style.css"> -->
    <style>
        .container{
    max-width: 80%; 
    padding: 34px; 
    margin: auto;
        }

        input{
            
            border: 2px solid black;
            border-radius: 6px;
            outline: none;
            font-size: 16px;
            width: 80%;
            margin: 11px 0px;
            padding: 7px;
        }

        form{
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }

        .btn{
            color: white;
            background: black;
            padding: 8px 12px;
            font-size: 20px;
            border: 2px solid white;
            border-radius: 14px;
            cursor: pointer;
        }
</style>
</head>
<body>
    <div class="container">
        <form action="main.php" method="post">
            <input type="text" name="string" id="string" placeholder="Enter the String">
            <button class="btn">Submit</button>
        </form>
    </div>    
</body>
</html>
