---
layout: post
title:  "Simple Login System With Codeigniter"
date:   2016-06-5
categories: Codeigniter
posted: haris
---

<p>Setelah sukses menginstall Codeingiter pada tutorial sebelum nya <a href="{% post_url  2016-05-31-welcome-to-jekyll %}" class="tags"><b>(Tutorial Installasi Codeigniter
    )</b></a>. Lanjut pada tutorial codeigniter kali ini saya akan share tutorial dan source code cara membuat login dengan codeigniter.</p>
<p>
    Tahapan pertama kita perlu membuat sebuah table dengan nama 'users', yang berisi 5 kolom (id,name,pasword,created_at,updated_at)


{% highlight sql %}

CREATE TABLE IF NOT EXISTS `users` (
`id` int(11) NOT NULL AUTO_INCREMENT,
`name` varchar(255) NOT NULL,
`password` varchar(255) NOT NULL,
`created_at` date,
`updated_at` date,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 AUTO_INCREMENT=2 ;

{% endhighlight %}







Selanjut nya kita perlu mengaktifkan library pendukung system login pada codeingiter :
<div class="col-lg-offset-1">
    <li>Iibrary database</li>
    <li>Iibrary sesion</li>
    <li>Set encryption key session </li>
    <li>Form Helper</li>
    <li>Url Helper</li>
</div>
buka file /application/config.php lalu edit seperti berikut ini
{% highlight php %}
<?php $this->load->view('v_home'); ?>

{% endhighlight %}
</p>


