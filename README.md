securimage_for_ci
=================


Install:

* Download the Securimage Library from http://doublekai.org/files/Securimage_For_CI.zip
* Copy file libraries / Securimage.php to application / libraries
* Copy file config / Securimage.php to application / config
* Copy dir views / fonts to application / views

if you want to quickstart test

* Copy file controlls / welcome.php to application / controlls
* Copy file controlls / image.php to application / controlls
* Copy file views / test.html to application / views


Example:

Controlls

- controllers / welcome.php
class Welcome extends Controller {
    function Welcome(){
        parent::Controller();
        $this->load->library('securimage');
        $this->load->helper('url');
        $this->load->helper('html');
    }
    function index(){
        $this->load->view('test.html');
    }
    function check(){
        $inputCode = $this->input->post('imagecode');
        if($this->securimage->check($inputCode) == true){
            $data['result'] = '<h1>=v= PASS!</h1>';
            $this->load->view('test.html',$data);
        } else {
            $data['result'] = '<h1>/_\ FAILURE</h1>';
            $this->load->view('test.html',$data);        
        }
    }
} 

- controllers / image.php
class Image extends Controller {
    function Image(){
        parent::Controller();
        $this->load->library('securimage');        
    }
    function securimage(){
        $this->securimage->show();
    }
} 


Views

- views / test.html
<?php echo $result?>
<form action="<?php echo site_url('welcome/check')?>" method="post">
   <?php echo img('image/securimage', TRUE)?><br/>
   <input type="text" name="imagecode" />
   <input type="submit" value="check" />
</form> 
 Signature 

