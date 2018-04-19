### Java HTTP 请求

> _**例 ：登录某个网站并获取cookies**_

```java
package messageoom_interface;

import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.HttpStatus;
import org.apache.http.NameValuePair;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.CookieStore;
import org.apache.http.client.HttpClient;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.impl.client.AbstractHttpClient;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.protocol.HTTP;
import org.apache.http.util.EntityUtils;
import org.json.JSONException;
import org.json.JSONObject;


/**
 * 
 * @author MessageOOM
 *
 */

public class httpPostTest {
	public final static Map meCookiesMap = new HashMap();
	private static final String meURL = "http://www.XXX.cn/index/login";
	static HttpClient meClient = new DefaultHttpClient();
	/**
	 * 
	 * @param args
	 * @throws ClientProtocolException
	 * @throws IOException
	 * @throws JSONException
	 * @author MessageOOM
	 */
	public static void main(String[] args) throws ClientProtocolException, IOException, JSONException{
		httpPostTest hPostTest = new httpPostTest();
		System.out.println(hPostTest.getCookies(meURL));
		}
	
	 /**
	  * login system and get cookies
	  * @param URL
	  * @throws ClientProtocolException
	  * @throws IOException
	  * @throws JSONException
	  * @author MessageOOM
	  */
	public static int getCookies(String URL) throws ClientProtocolException, IOException, JSONException{
		int responseCode = 0;
		
		HttpPost meHttpPost = new HttpPost(URL);
		List <NameValuePair> params = new ArrayList<NameValuePair>();
		params.add(new BasicNameValuePair("loginusername", "xxxxxx"));
		params.add(new BasicNameValuePair("loginpassword", "xxxxxx"));
		meHttpPost.setEntity(new UrlEncodedFormEntity(params,HTTP.UTF_8));
		HttpResponse  response = meClient.execute(meHttpPost);
		CookieStore meCookie = ((AbstractHttpClient) meClient).getCookieStore();
		
		if(response.getStatusLine().getStatusCode() == 200){
			String entity = EntityUtils.toString(response.getEntity());
			JSONObject json = new JSONObject(entity);  
		        responseCode = (int) json.get("code");
		        //System.out.println(entity);
			List listCookies = meCookie.getCookies();
			for (int i = 0; i < (listCookies.size()); i++) {
				String meCookieKey = meCookie.getCookies().get(i).getName();
				String meCookieValue = meCookie.getCookies().get(i).getValue();
				meCookiesMap.put(meCookieKey, meCookieValue);
				}
			//System.out.println(meCookiesMap);
			}
		else {
			System.out.print("please check request parameters");
			}
		//System.out.println(meCookiesMap);
		return responseCode;
		}

}



```



