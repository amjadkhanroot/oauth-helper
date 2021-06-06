# oauth-helper
A library for generate OAuth V1 signatures in PHP.

-Requirements:
PHP 5.3.0 or higher

-Usege:

For Laravel:

    //import it
    use App\Http\Controllers\OAuthV1 as OAuthV1;

    //Test class
    class Test extends Controller
    {
  
 
      //Test function
      public function testOAuth()
      {
          //Set the required variables:
          $params = [];
          $httpMethod = "POST";
          $url = "http://www.test.com/api/create"
          $nonce = sha1(random_bytes(32));
          $timestamp = now()->timestamp;

          //Pass it to the lib:
          OAuthV1::setConsumerKey("TestTest", "TestTest");
          $ov = OAuthV1::getInstance();
          $ov->setToken("******", "******");
          $ov->setParams($params);

          // Generate the string and set it to your header:
          $authorization = $ov->sign($httpMethod, $url, $timestamp, $nonce);
          $val = $ov->validate($authorization, $httpMethod, $url);
          dd($val);
     }
    }
    
-Output

      $authorization: "OAuth oauth_consumer_key="TestTest", oauth_nonce="76ba30098c425f9d202b2ef4ebcbc8bbef60fe38", oauth_signature="M9UtVEogXThRnOp4Gx1H3mPnDTQ%3D", oauth_signature_method="HMAC-SHA1", oauth_timestamp="1622958567", oauth_token="%252A%252A%252A%252A%252A%252A", oauth_version="1.0""
      
      $val: true
      
          
