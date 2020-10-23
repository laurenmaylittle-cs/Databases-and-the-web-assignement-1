# Databases-and-the-web-assignement-1

<!DOCTYPE html>
<html>
<head>
<title>Gym Membership</title>
<style type = "text/css">
	.T1table{
		width: 50%;
	}
	.T1table tr {
		background: #e0eeef
	}
	.T1table tr:nth-child(odd){
		background: #e0eeef
	}
	.T1table tr:nth-child(even){
		background: #d3d3d3
	}
th {
  height: 25px;
}
tr {
  height: 25px;
}
</style>

</head>

<body>
<form id="mainForm" name = "mainForm">
Name: <input id = "yourname" name ="yourname" type = "text" /><br />
Age: <input id = "age" name="age" type="number" /><br />
Height: Feet: <select id = "HeightInFeet" name = "HeightInFeet">
	<option value ="4"> 4</option>
	<option value ="5"> 5</option>
	<option value ="6"> 6</option>
</select>
Inches: <select id = "HeightInInches" name = "HeightInInches">
	<option value ="0"> 0</option>
	<option value ="1"> 1</option>
	<option value ="2"> 2</option>
	<option value ="3"> 3</option>
	<option value ="4"> 4</option>
	<option value ="5"> 5</option>
	<option value ="6"> 6</option>
	<option value ="7"> 7</option>
	<option value ="8"> 8</option>
	<option value ="9"> 9</option>
	<option value ="10">10</option>
	<option value ="11">11</option>
</select><br />
Start date: <input id = "startdate" name ="startdate" type="date" /><br/><br/>
<input type ="button" value ="Display" onClick ="submitForm();"/>
<input type="reset" value="Reset">
</form></br>
<table id = "dataTable" class = "T1table">
<caption>Row Count</caption>
	<tr> <th>Name</th> <th>Age</th> <th>Height</th> <th>Start Date</th> <th>Delete</th>
</table>

<script>
function updateCaption() {
	document.getElementById("dataTable").deleteCaption();
	var rowCount = document.getElementById("dataTable").rows.length - 1;
	var table = document.getElementById("dataTable").createCaption();
	table.innerHTML = "Row Count = " + rowCount;
}

function submitForm()
{
	//var nameValid = checkName(document.getElementById("yourname").value);
	var ageValid = checkAge(document.getElementById("age").value);
	var dateValid = checkDate(document.getElementById("startdate").value);
	
	if (dateValid && ageValid) {
		// Data is valid - add row to table
		addRow();
		// Update caption
		updateCaption();
		// Reset form
		var formName = document.getElementById("mainForm");
		formName.reset();
	}
}

function checkName(name) 
{
	var invalid = /[^a-z A-Z]/;
	if (name == "" || invalid.test(name)) {
		alert( "Please enter a valid name");
		return false;
	}
	return true;
}

function checkAge(str) 
{
	age = parseInt(str);
	if ( isNaN(age) || age < 18 || age >60) {
		alert( "Age entered is not valid (must be between 18 & 60)");
		return false;
	}
   return true;
}

function checkDate(date)
{
	var d = new Date(date);
	var year = d.getFullYear();
	if (year != 2020 ){
		alert("Start date must be in 2020");
		return false;
	}
	return true;
}
function addRow() 
{
	var table = document.getElementById('dataTable');
	var tr = table.insertRow(1);
	var bcolor;
	var rowCount = document.getElementById("dataTable").rows.length - 1;
	
	if (rowCount % 2 == 1){
		bcolor = "#e0eeef";
	}
	else{
		bcolor = "#d3d3d3";
	}
	
	var td = document.createElement('td');
	td = tr.insertCell(0)
	var e = document.createElement('input');
    e.setAttribute('type', 'text');
	e.style.backgroundColor = bcolor;
    e.setAttribute('value', document.getElementById("yourname").value);
	td.appendChild(e);
	
	var td = document.createElement('td');
	td = tr.insertCell(1)
	var e = document.createElement('input');
    e.setAttribute('type', 'text');
	e.style.backgroundColor = bcolor;
    e.setAttribute('value', document.getElementById("age").value);
	td.appendChild(e);
	
	var td = document.createElement('td');
	td = tr.insertCell(2)
	var e = document.createElement('input');
    e.setAttribute('type', 'text');
	e.style.backgroundColor = bcolor;
    e.setAttribute('value', document.getElementById("HeightInFeet").value + " " + document.getElementById("HeightInInches").value);
	td.appendChild(e);
	
	var td = document.createElement('td');
	td = tr.insertCell(3)
	var e = document.createElement('input');
    e.setAttribute('type', 'text');
	e.style.backgroundColor = bcolor;
    e.setAttribute('value', document.getElementById("startdate").value);
	td.appendChild(e);
	
	var td = document.createElement('td');
	td = tr.insertCell(4)
    var button = document.createElement('input');
    button.setAttribute('type', 'button');
    button.setAttribute('value', 'Delete');
    button.setAttribute('onclick', 'deleteRow(this)');
    td.appendChild(button);
}

function deleteRow(row)
{
	var i = row.parentNode.parentNode.rowIndex;
	document.getElementById("dataTable").deleteRow(i);
	updateCaption();
}
   
</script>
</body>

</html>
