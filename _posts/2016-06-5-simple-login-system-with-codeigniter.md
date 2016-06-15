---
layout: post
title:  "Simple Login System With Codeigniter"
date:   2016-06-5
categories: Codeigniter
posted: haris
---
Setelah sukses menginstall Codeingiter pada tutorial sebelum nya <a href="{% post_url  2016-05-29-installasi-codeigniter %}" class="tags"><b>(Tutorial Installasi Codeigniter
    )</b></a>. Lanjut pada tutorial codeigniter kali ini saya akan share tutorial dan source code cara membuat login dengan codeigniter.

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

Lalu buat username dan password nya
{% highlight sql%}
insert into users (name, password) values ('admin', MD5('admin'));
{% endhighlight %}

buka file /application/config.php lalu edit line seperti berikut ini
{% highlight php %}
<?php

...........

$config['base_url'] = rtrim(dirname($_SERVER['SCRIPT_NAME']), '/') . '/';

$config['index_page'] = '';

$config['encryption_key'] = 'Isi_dengan_yang_anda_inginkan';

...........

{% endhighlight %}

 Buka file /application/autoload.php lalu edit line seperti berikut ini:
    {% highlight php %}
<?php

...........

$autoload['libraries'] = array('database','session','form_validation');

$autoload['helper'] = array('url','file','form');

...........

{% endhighlight %}

Buka file /application/database.php lalu edit line sesuaikan dengan database yang anda gunakan:
    {% highlight php %}
<?php

...........

$db['default']['hostname'] = 'localhost';
$db['default']['username'] = 'yourdbusername';
$db['default']['password'] = 'yourdbpassword';
$db['default']['database'] = 'yourdbname';

...........

{% endhighlight %}


Buka file /application/routes.php lalu edit line seperti berikut ini:
    {% highlight php %}
<?php

...........

$route['default_controller'] = "login";

...........

{% endhighlight %}


Setelah kita rubah default controller menjadi "login" ,dimana "login" adalah controllers yang pertama kali akan di panggil. Buatlah sebuah file di folder
    /application/controllers/login.php
    {% highlight php %}
<?php if (!defined('BASEPATH')) exit('No direct script access allowed');

class Login extends CI_Controller {
    function __construct()
    {
        parent::__construct();
        $this->load->helper(array('form'));

    }

    function index()
    {
        $this->load->view('v_Login');
    }



}

{% endhighlight %}


Buat file "v_Login.php" pada folder /application/views/v_Login.php

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>CodeIgniter</title>

    <!-- Fonts -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.4.0/css/font-awesome.min.css" rel='stylesheet' type='text/css'>
    <link href="https://fonts.googleapis.com/css?family=Lato:100,300,400,700" rel='stylesheet' type='text/css'>

    <!-- Styles -->
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            font-family: 'Lato';
        }

        .fa-btn {
            margin-right: 6px;
        }
    </style>
</head>


<body id="app-layout">
<nav class="navbar navbar-default">
    <div class="container">
        <div class="navbar-header">

            <!-- Collapsed Hamburger -->
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#spark-navbar-collapse">
                <span class="sr-only">Toggle Navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>

            <!-- Branding Image -->
            <a class="navbar-brand" href="#">
                CodeIgniter
            </a>
        </div>

        <div class="collapse navbar-collapse" id="spark-navbar-collapse">
            <!-- Left Side Of Navbar -->
            <ul class="nav navbar-nav">
                <li><a href="<?php echo site_url('welcome')?>">Welcome</a></li>
            </ul>

            <!-- Right Side Of Navbar -->
            <ul class="nav navbar-nav navbar-right">
                <!-- Authentication Links -->
                <li><a href="<?php echo site_url('login')?>">Login</a></li>
                <li><a href="<?php echo site_url('register')?>">Register</a></li>

            </ul>
        </div>
    </div>
</nav>
<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">

            <div class="alert alert-danger <?php if($this->session->flashdata('error') =='') echo  'hide'; ;?>">
                <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
                <strong>Error!</strong> <?php echo $this->session->flashdata('error');?>
            </div>
            <div class="panel panel-default">

                <div class="panel-heading">Login</div>
                <br/>
                <form class="form-horizontal" role="form" method="post" action="<?php echo site_url('VerifyLogin')?>">

                    <div class="form-group ">
                        <label class="col-md-4 control-label">Username</label>

                        <div class="col-md-6">
                            <input type="text" class="form-control" name="username">

                        </div>
                    </div>

                    <div class="form-group ">
                        <label class="col-md-4 control-label">Password</label>

                        <div class="col-md-6">
                            <input type="password" class="form-control" name="password">
                        </div>
                    </div>

                    <div class="form-group">
                        <div class="col-md-6 col-md-offset-4">
                            <div class="checkbox">
                                <label>
                                    <input type="checkbox" name="remember"> Remember Me
                                </label>
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <div class="col-md-6 col-md-offset-4">
                            <button type="submit" class="btn btn-primary">
                                <i class="fa fa-btn fa-sign-in"></i>Login
                            </button>

                            <a class="btn btn-link" href="<?php echo site_url('#')?>">Forgot Your Password?</a>
                        </div>
                    </div>
                </form>
                <div class="panel-body"></div>
            </div>
        </div>
    </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</body>
</html>

{% endhighlight %}


Buat file "verifylogin.php" pada controllers
{% highlight php %}
<?php if (!defined('BASEPATH')) exit('No direct script access allowed');
class VerifyLogin extends CI_Controller {
    function __construct()
    {
        parent::__construct();
        $this->load->model('user', '', TRUE);
    }

    function index()
    {
    //This method will have the credentials validation
    $this->load->library('form_validation');

    $this->form_validation->set_rules('username', 'Username', 'trim|required|xss_clean');
    $this->form_validation->set_rules('password', 'Password', 'trim|required|xss_clean|callback_check_database');

    if ($this->form_validation->run() == FALSE) {
    //Field validation failed.  User redirected to login page
    $this->load->view('v_Login');
        } else {
        //Go to private area
        redirect('home', 'refresh');
        }

    }

    function check_database($password)
    {
    //Field validation succeeded.  Validate against database
    $username = $this->input->post('username');

    //query the database
    $result = $this->user->login($username, $password);

    if ($result) {
        $sess_array = array();
        foreach ($result as $row) {
            $sess_array = array(
                'id'       => $row->id,
                'username' => $row->username);

            $this->session->set_userdata('logged_in', $sess_array);
        }
        return TRUE;
    } else {
        $this->form_validation->set_message('check_database', 'Invalid username or password');
        return false;
        }
    }

}

{% endhighlight %}

Buat lah file "login.php" pada folder models , untuk mengambil data user dari database

{% highlight php %}

<?php

Class User extends CI_Model{
 function login($username, $password)
 {
    $this -> db -> select('id, username, password');
    $this -> db -> from('users');
    $this -> db -> where('username', $username);
    $this -> db -> where('password', MD5($password));
    $this -> db -> limit(1);

    $query = $this -> db -> get();

        if($query -> num_rows() == 1)
        {
            return $query->result();
        }else{
            return false;
        }
 }

}

{% endhighlight %}

Buat file "home.php" pada controllers

{% highlight php %}
<?php if (!defined('BASEPATH')) exit('No direct script access allowed');

session_start(); //we need to call PHP's session object to access it through CI
class Home extends CI_Controller {

    function __construct()
    {
        parent::__construct();
    }


    function index()
    {
        if ($this->session->userdata('logged_in')) {
            $session_data = $this->session->userdata('logged_in');
            $data['username'] = $session_data['username'];
                $this->load->view('v_Home', $data);
        } else {
        //If no session, redirect to login page
        redirect('login', 'refresh');
        }
    }


    function logout()
    {
        $this->session->unset_userdata('logged_in');
        session_destroy();
        redirect('home', 'refresh');
    }

}


{% endhighlight %}

Buat file "v_Home.php" pada folder views

{% highlight php %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>CodeIgniter</title>

    <!-- Fonts -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.4.0/css/font-awesome.min.css" rel='stylesheet' type='text/css'>
    <link href="https://fonts.googleapis.com/css?family=Lato:100,300,400,700" rel='stylesheet' type='text/css'>

    <!-- Styles -->
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            font-family: 'Lato';
        }

        .fa-btn {
            margin-right: 6px;
        }
    </style>
</head>


<body id="app-layout">
<nav class="navbar navbar-default">
    <div class="container">
        <div class="navbar-header">

            <!-- Collapsed Hamburger -->
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#spark-navbar-collapse">
                <span class="sr-only">Toggle Navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>

            <!-- Branding Image -->
            <a class="navbar-brand" href="#">
                CodeIgniter
            </a>
        </div>

        <div class="collapse navbar-collapse" id="spark-navbar-collapse">
            <!-- Left Side Of Navbar -->
            <ul class="nav navbar-nav">
                <li><a href="<?php echo site_url('home')?>">Dashboard</a></li>
            </ul>

            <!-- Right Side Of Navbar -->
            <ul class="nav navbar-nav navbar-right">
                <!-- Authentication Links -->
                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-expanded="false">
                        <?php echo $user?> <span class="caret"></span>
                    </a>

                    <ul class="dropdown-menu" role="menu">
                        <li><a href="<?php echo site_url('auth/logout')?>"><i class="fa fa-btn fa-sign-out"></i>Logout</a></li>
                    </ul>
                </li>

            </ul>
        </div>
    </div>
</nav>
<div class="container spark-screen">
    <div class="row">
        <div class="col-md-10 col-md-offset-1">
            <div class="panel panel-default">
                <div class="panel-heading">Dashboard</div>

                <div class="panel-body">
                    You are logged in!
                </div>
            </div>
        </div>
    </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
</body>
</html>

{% endhighlight %}

