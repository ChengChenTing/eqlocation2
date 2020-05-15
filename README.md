# eqlocation2
Locating earthquake by importing coordinates and magnitude from USGS json file


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Earthquake input from Json file</title>
</head>
<body>
<h2>Earthquake input from Json file</h2>
<p id="coordinates"></p><br>
<div class="coordinates"></div>
<button id="btn">Get Json File</button>

<script>
  document.getElementById('btn').addEventListener('click', loadtext)

  function loadtext(){
    // console.log('button clicked!!!');
     
    var xhr= new XMLHttpRequest();
    // console.log(xhr);
    // OPEN - type, url/file, async
    xhr.open('GET', 'earthquake.json', true);

    var output='';

    xhr.onload= function(){
      if(this.status==200){
         // console.log(this.responseText);   
         var resp= this.responseText;
         console.log(resp);

         myObj= JSON.parse(resp);
         // console.log(myObj);
         console.log(typeof myObj);
         console.log(myObj.length);

           for (var i=0; i < myObj.length; i++){
           //console.log(myObj[i].geometry.coordinates);  
           //console.log(myObj[i].properties.mag);   

           console.log('lat:' + myObj[i].geometry.coordinates[0] + " ; " +
                       'lng:' + myObj[i].geometry.coordinates[1] + " ; " +
                       'mag:' + myObj[i].properties.mag)

          output +=myObj[i].geometry.coordinates[0] + " ; " +
                   + myObj[i].geometry.coordinates[1] + " ; " +
                   + myObj[i].properties.mag + " | ";

          output +=
          '<div class="coordinates">' +
          '<ul>' +
          '<li>Latitude: '+myObj[i].geometry.coordinates[0]+' </li>' +
          '<li>Longitude: '+myObj[i].geometry.coordinates[1]+' </li>' +
          '<li>magitude: '+myObj[i].properties.mag+' </li>' +
          '</ul>' +
          '</div>';

          document.getElementById('coordinates').innerHTML= output;
     
         }     
          event_str=JSON.stringify(output);
          console.log(typeof output);
          //console.log(output);
          localStorage.setItem('eqEvents', output)   
      }
     }
    // Send request
    xhr.send();
  }
  
// Http status
// 200: OK
// 403: "Forbidden"
// 404: "Not found"

</script>
  
</body>
</html>
