```
<html>
<body>
<h2>Read a text file and display the content</h2><br>
 <form action="index.php" method="post"
      enctype="multipart/form-data">      
            <input type="file" name="file" id="file">
	    <br>   
            <input type="submit" name="submit" value="Submit">
    </form
<?php
if ( $_SERVER['REQUEST_METHOD'] == 'POST' ) {
if ($_FILES["file"]["type"] == "text/plain" &&
    $_FILES["file"]["size"] < 65536)
{
  if ($_FILES["file"]["error"] > 0)
  {
    echo "Error: " . $_FILES["file"]["error"] . "<br>";
  }
  else
  {
    
    echo "Type: " . $_FILES["file"]["type"] . "<br> ";
    echo "Size: " . ($_FILES["file"]["size"] / 1024) . " Kb<br>";
   
    if (file_exists("upload/" . $_FILES["file"]["name"]))
    {
      echo $_FILES["file"]["name"] . " already exists. ";
    }
    else
    {
      move_uploaded_file($_FILES["file"]["tmp_name"],
      "/tmp/" . $_FILES["file"]["name"]);
        echo "<!--Saved as: " . "/tmp/" . $_FILES["file"]["name"] . "-->";
	//readfile(. "upload/" . $_FILES["file"]["name"]);
	echo "<br><br>File content:<br><br>";
	echo htmlentities(file_get_contents("/tmp/" . $_FILES["file"]["name"]));
	unlink("/tmp/" . $_FILES["file"]["name"]);
	echo "<br<br>><hr>File deleted";
    }
  }
}
else
{
 
     if ($_FILES["file"]["type"] != "text/plain")
   	 echo "<h1>File is not of the permitted type.</h1>";
     else if ($_FILES["file"]["size"] < 65536)
  	 echo "<h1>File exceeds permitted size.</h1>";
}
}
?> 
 </body>
</html>
```
