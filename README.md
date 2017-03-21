### What is jQuery?

jQuery is an (extremely) popular JavaScript library. jQuery makes it much easier to find and change html elements, and do stuff in response to user events to make webpages more interactive.

### SET UP:

- Download zip file from here: https://github.com/daneasterman/decoded-wishlist

- Open up the files in text editor (sublime), then open up the index.html file in Chrome, right click anywhere on page and hit inspect element, then toggle to console.

### Step 1 - Append

Add item to the page using simple append: 

```
$('#items').append('<li>My first item</li>');
```
  
### Step 2 - Grab Val() in input element

Grab the content in the val() input field: Get the content and then change it using val in console.

```
$('#item').val();

$('#item').val('Any text here');

```
  
### Step 3 - Add click handler, put val() code inside

```
$(document).on('click', '#add-to-list', function() {
  var value = $('#item').val();
  $('#items').append('<li>' + value + '</li>');  
});
```

### Step 4 - Iterate! - Make some small improvements

We want the input field to clear every time we add an item:

Add this line:

```
$('#item').val("");
```

We also want input field to automatically focus:

```
$('#item').focus();
```

### Step 5: Use the keyboard "enter" button to add an item:

```
$(document).keypress(function(event) {
  if ( event.which == 13 ) {
    addToList();
  }
});
```

### Step 6: Let's refactor to make code DRY:
Let's put our append code in addToList function:

```
function addToList() {
}
```

### Step 7: Add Pending Labels!

```
  $('#items').append('<li>' + value + '<span class="label pending">Pending</span></li>');
```

### Step 8: Add Click Handler to the Label!

```
$(document).on('click', '.pending', function() {
  var parentLi = $(this).parent();
  $(parentLi).find('.pending').remove();
  parentLi.append('<span class="label success">Done!</span>');
  });
  ```

### Step 8: Add Completed class (strikethrough )

```
parentLi.addClass('completed');
```

### Step 9: Add Running totals pending and completed items:

```
function updateTotal() {
  var pendingLength = $('.pending').length;
  var completedLength = $('.completed').length;
  $('.total').text('Pending: ' + pendingLength + '  Completed: ' + completedLength);
}
```

Add the update total function inside our `.pending` click handler and our `funtion addToList() { }`:

```
updateTotal();
```

### Credits:

This tutorial is inspired and adapted from the jQuery tutorial from codebar.io, find the original one (without all the answers) here: [http://tutorials.codebar.io/js/lesson3/tutorial.html](http://tutorials.codebar.io/js/lesson3/tutorial.html).