# wp-basic-concept


###  WordPress এ Hook কি?

Hook গুলো অনেকটা ওয়ার্ডপ্রেসের মেরুদন্ড এর মতো কাজ করে। যা আপনাকে ওয়ার্ডপ্রেস core file এ কোনো ধরণের পরিবর্তন না করেই নিজের তৈরী ফাঙ্কশন দিয়ে ওয়ার্ডপ্রেস এ যেকোনো ধরণের নতুন ফীচার যুক্ত অথবা ডিফল্ট ফীচার কে পরিবর্তনের জন্য সুযোগ দেয়। আরো সহজভাবে বলা যায় , wordpress এ hooks system হচ্ছে এক ধরণের api system যা আপনাকে নিজের তৈরী php function ওয়ার্ডপ্রেস এ রান করার সুযোগ দেয়। পুরো ওয়ার্ডপ্রেসই দাঁড়িয়ে আছে এই Hook এর উপরে। WordPress এ hook দুই ধরণের: একটা হচ্ছে WordPress Action Hook এবং অন্যটি হচ্ছে filters hook.


 ### Actions Hook
WordPress Action Hook গুলো আপনাকে আপনার WordPress সাইট লোডিং এর সময় অথবা আপনার ওয়ার্ডপ্রেস সাইটের কোনো একটা ইভেন্ট এ একটা নির্দিষ্ট পয়েন্টে অতিরিক্ত ফাঙ্কশনালিটি বা ফীচার যুক্ত করার জন্য যেকোনো কাস্টম ফাঙ্কশনকে রান করার সুযোগ দেয় । যেমন : আপনি যদি একটা অতিরিক্ত widgets অথবা menus যুক্ত করতে চান, অথবা আপনার সাইটে একটা প্রমোশনাল মেসেজ যুক্ত করতে চান, তাহলে আপনাকে action hook ব্যবহার করতে হবে।

WordPress Action Hook গুলো নিয়ে কাজ করার জন্য আপনাকে কয়েকটি ফাঙ্কশন সম্পর্কে স্পষ্ট ধারণা থাকতে হবে। এর মধ্যে অন্যতম দুটি ফাঙ্কশন হচ্ছে do_action() এবং add_action() function দুটি। চলুন প্রথমে এই দুটি ফাঙ্কশন নিয়ে আলোচনা করা যাক।

do_action() vs add_action()
মূলতঃ ওয়ার্ডপ্রেসে যেকোনো নতুন custom action hook রেজিস্টার করার জন্য do_action() function টি ব্যবহৃত হয়। আর do_action() দিয়ে রেজিস্টারকৃত যেকোনো custom action hook অথবা WordPress built-in যেকোনো Action hook এর জন্য একটা callback function যুক্ত করার জন্য add_action() function টি ব্যবহৃত হয়। আবার অন্যভাবে বলা যায়, add_action() মেথড দিয়ে সেট করা hook কে অথবা hook এর রেজাল্টকে দেখানোর জন্য আমরা do_action() function টি ব্যবহার করব। উল্লেখ্য, do_action() function টি আপনি plugin এবং theme দুই জায়গাতেই আপনি ব্যবহার করতে পারেন। এবার চলুন প্রথমে do_action() ফাঙ্কশন টি কিভাবে কাজ করে , সেটি দেখা যাক।

```php
do_action( string $tag, mixed $arg );
```

$tag: (string) (Required) যেই action hook টি execute করবেন সেটির নাম।
$arg:(mixed) (Optional) action hook টির জন্য যত ইচ্ছা ততগুলো প্যারামিটার পাঠাতে পারবেন, আবার চাইলে একটাও না পাঠাতে পারেন। ডিফল্ট ভাবে খালি থাকে। আর এই সবই নির্ভর করবে , আপনার add_action() ফাঙ্কশনে ব্যবহৃত callback ফাঙ্কশনের উপর। অর্থাৎ , সেই callback function এ আবশ্যক কোনো parameter থাকে , তাহলে তার জন্য অবশ্যই argument পাঠাতে হবে।
নিচে কোনো প্যারামিটার ছাড়া একটা do_action() ফাঙ্কশনের উদাহরণ দেওয়া হলো।

```php

<?php
do_action( 'display_bangla_quotes' );
?>

```

এখন আপনি চাইলে উপরের লাইনটি আপনার থিম অথবা প্লাগিনে যেকোনো জায়গায় ব্যবহার করতে পারেন, তবে “display_bangla_quotes” এই হুক ট্যাগ টি অবশ্যই add_action() ফাঙ্কশন দিয়ে তৈরি একটা action হুক হতে হবে। এই বিষয়ে আমরা কিছুক্ষন পরে একটা পরিপূর্ন উদাহরণ দিবো। তার আগে চলুন add_action() ফাঙ্কশন টি কিভাবে কাজ করে , সেটি দেখা যাক।


### Actions Functions

* has_action()
* add_action()
* do_action()
* do_action_ref_array()
* did_action()
* remove_action()
* remove_all_actions()
* doing_action()



### WordPress এ Filter Hook কি?

WordPress এ Filter Hook গুলি Action Hook গুলোর চেয়ে অনেক বেশি আলাদা। সাধারণত, WordPress এ নতুন কোনো ফীচার বা ফাঙ্কশনালিটি যুক্ত করার জন্য Action Hook গুলো ব্যবহৃত হয় , আর অন্যদিকে Filter Hook গুলো আপনাকে ওয়ার্ডপ্রেসের রান টাইম কোডের আউটপুট ম্যানিপুলেট বা যেকোনো পরিবর্তনের সুযোগ সৃষ্টি করে। আরো সহজে বলা যায় Action Hook গুলি আপনাকে নতুন ফীচার বা ফাঙ্কশনালিটি যুক্ত করতে সাহায্য করে, আর filter Hook গুলো আপনাকে Action Hook দিয়ে তৈরী ফীচার বা ফাঙ্কশনালিটি গুলো পরিবর্তন করতে সাহায্য করবে। এক কোথায় আপনার Action Hook এর Output কে “filter” করবে।

ওয়ার্ডপ্রেসে Filter hook গুলো নিয়ে কাজ করার জন্য আপনাকে কয়েকটি ফাঙ্কশন সম্পর্কে স্পষ্ট ধারণা থাকতে হবে। এর মধ্যে অন্যতম দুটি ফাঙ্কশন হচ্ছে add_filter() এবং apply_filters() function দুটি। চলুন প্রথমে এই দুটি ফাঙ্কশন নিয়ে আলোচনা করা যাক।



### Filter Functions:

* has_filter()
* add_filter()
* apply_filters()
* apply_filters_ref_array()
* current_filter()
* remove_filter()
* remove_all_filters()
* doing_filter()



### Activation/Deactivation/Uninstall Functions

* register_activation_hook()
* register_uninstall_hook()
* register_deactivation_hook()


