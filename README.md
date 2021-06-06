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
          $oauth = $ov->sign($httpMethod, $url, $timestamp, $nonce);
          dd($oauth);
     }
    }
