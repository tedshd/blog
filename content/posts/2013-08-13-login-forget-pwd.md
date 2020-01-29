---
layout: post
title: 'Login forget pwd'
date: 2013-08-13
comments: true
categories:
---
## function

* account
* captcha
* validation
* use bootatrap model

## result

* captcha fail
* captcha ok
* backend check account
 * success
 * fail(not exist)

## method

* ajax

## mockup
[link](https://moqups.com/tedshd/guwR4fO3/)

## flow
click forget password
show model
enter account & captcha(validation from js not null)
submit(ajax)
account fail(from backend) -> show message
captcha fail(from backend) -> show message
success -> show message

## flow(detail)
點擊忘記密碼
秀 bootstrap model
輸入帳號與驗證碼(利用 validation 作必填的檢查)
用 ajax 的方式送出

* controllers
 * ~~接 captcha -> 檢查是否正確~~
 * 接 account ->
     * ~~檢查是否存在~~
     * ~~generator token~~
     * save token to memcache
     		* memcache key: token + account
     * send email

回傳錯誤或成功訊息

* ~~account 驗證失敗 -> 秀訊息(該帳號不存在)~~
* ~~captcha 驗證失敗 -> 秀訊息(驗證碼失敗), 刷新驗證碼~~

email incloud url

* url + account + token

**URL**
點擊 URL
進入重設密碼頁面

* 新密碼(利用 validation 作必填的檢查)
* 確認密碼(利用 validation 作必填的檢查)

用 submit 的方式送出

* controllers
 * 接新密碼 ->
 		* 驗證
 		* 存 DB
		* delete memcache

回傳成功或失敗

* 成功 -> redirect 到成功頁面
* 失敗 -> 秀訊息(儲存失敗, 請再試一次)

### token verify

#### gen token

```PHP
// load memcache
$this->load->library('Memcache');
// load encrypt
$this->load->library('encrypt');

$token = array(
    'rand_str' => md5(uniqid(rand(), true)),
    'account' => $user,
);
// array to string
$to_str = serialize($token);
// encrypt
$encrypted_str = $this->encrypt->encode($to_str);
// save to memcache
$this->memcache->set('key', $encrypted_str);

// token to verify
token['rand_str']
```

#### get and verify data

```PHP
// get $encrypted_str
// decode
$decode_token = $this->encrypt->decode($encrypted_str);
// string to array
$token = unserialize($decode_token);
// check $token exist
if ($token['rand_str'])
$get_token = token['rand_str'];
$account
// load memcache
$load_mem = $this->memcache->get('key');
// decode memcache
$decode_mem = $this->encrypt->decode($load_mem);
// string to array
$to_array = unserialize($decode_mem);
// verify
$get_token === $to_array['rand_str']
$account === $to_array['account']
```
