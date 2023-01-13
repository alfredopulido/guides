# HTML Frontend

**Colocar en header:**
`<script src='https://www.google.com/recaptcha/api.js' async defer></script>`

**Colocar el div del recaptcha**
`<div class="g-recaptcha" data-sitekey="Site-key-Number"></div>`

# PHP Backend

    <?php
    	if(isset($_POST['g-recaptcha-response'])){
    		$captcha=$_POST['g-recaptcha-response'];
    	}
    	if(!$captcha){
    		echo 'Please check the the captcha form.';
    		$error = 'No se pudo enviar el mensaje.'; 
    	} else{
    		$secretKey = "Secret-Key-Number";
    		$ip = $_SERVER['REMOTE_ADDR'];
    		// post request to server
    		$url = 'https://www.google.com/recaptcha/api/siteverify?secret=' . urlencode($secretKey) .  '&response=' . urlencode($captcha);
    		function curl_get_file_contents($URL)
    		{
    			$c = curl_init();
    			curl_setopt($c, CURLOPT_RETURNTRANSFER, 1);
    			curl_setopt($c, CURLOPT_URL, $URL);
    			$contents = curl_exec($c);
    			curl_close($c);
    
    			if ($contents) return $contents;
    			else return FALSE;
    		}
    		//Si no existe get_file_contents usar curl
			$response = curl_get_file_contents($url);
    		$responseKeys = json_decode($response,true);
    		// should return JSON with success as true
    		if($responseKeys["success"]) {
    			/* Codigo para enviar correo */
    		}
    	}
    ?>

###End
