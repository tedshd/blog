---
layout: post
title: 'Codeigniter - AJAX(post)'
date: 2013-08-29
comments: true
categories: [codeigniter]
---
## CI AJAX(Post)

### Usage

JavaScript(jQuery)
```javascript
$.post(
    '/api/post',
    {
        val: 'string',
        val2: 1
    },
    function(data) {
        console.log(data);
        if(data.status === 'ok') {
            // dosomething
        } else {
            // alert fail
        }
    },
    'json'
);
```

```javascript
$.ajax({
  url: '/login/signup',
  type: 'POST',
  data: {
  	account: $('input[name="account"]').val()
  },
  success: function(data) {
  	console.log(data);
  }
});
```

PHP
```php
<?php

// api.php
public function post()
{
    $val = $this->input->post('val');
    $val2 = $this->input->post('val2');

    if ($val)
    {
        // dosomething

        //response
        $output = array(
            'status' => 'ok',
            'msg' => 'success'
        );
        echo json_encode($output);
        exit;
    }
    $output = array(
        'status' => 'fail',
        'msg' => 'error'
    );
    echo json_encode($output);
    exit;
}

?>
```
