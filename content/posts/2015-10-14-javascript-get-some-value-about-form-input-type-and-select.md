---
layout: post
title: 'JavaScript - Get & Set some value about form input type and select'
date: 2015-10-14
comments: true
categories: [javascript]
---
## JavaScript - Get some value about form input type and select

### Select

```html
<select id="select_data">
  <option value="1">test1</option>
  <option value="2" selected="selected">test2</option>
  <option value="3">test3</option>
</select>
```

```javascript
var e = document.getElementById('select_data');
var strUser = e.options[e.selectedIndex].value;
```

If want to set selected

```javascript
var e = document.getElementById('select_data');
e.querySelectorAll('option')[2].selected = true;
```

Get change option

```javascript
document.querySelector('#select_data').addEventListener('change', function (e) {
	var _this = this.options[this.selectedIndex];
});
```

### radio

```html
<div class="row">
  <p class="col">device</p>
  <div class="row col s12 m2">
    <input name="group1" type="radio" id="device_water_1" value="1" checked />
    <label for="device_water_1">True</label>
  </div>
  <div class="row col s12 m2">
    <input name="group1" type="radio" id="device_water_2" value="2" />
    <label for="device_water_2">False</label>
  </div>
</div>
```

```javascript
// for IE9 up
var val = document.querySelector('input[name="group1"]:checked').value;

// full support
var rates = document.getElementsByName('rate');
var rate_value;
for(var i = 0; i < rates.length; i++){
  if(rates[i].checked){
  	rate_value = rates[i].value;
  }
}
```

[Refer - html select - Get selected value in dropdown list using JavaScript? - Stack Overflow](http://stackoverflow.com/questions/1085801/get-selected-value-in-dropdown-list-using-javascript)

[Refer - javascript - How to get value of selected radio button? - Stack Overflow](http://stackoverflow.com/questions/15839169/how-to-get-value-of-selected-radio-button)
