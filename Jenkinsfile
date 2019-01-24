#!/usr/bin/env groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper
import javax.net.ssl.HostnameVerifier
import javax.net.ssl.HttpsURLConnection
import javax.net.ssl.SSLContext
import javax.net.ssl.TrustManager
import javax.net.ssl.X509TrustManager
import java.security.SecureRandom
import java.net.URLEncoder







	stage('Smoke Test') {


	        serviceName = 'maingateway-service'
		smokeTestOperation='cicd/maingateway/profile/11111?alertType=ACCIDENT'
		makeGetRequest("http://${serviceName}/${smokeTestOperation}")

 		serviceName = 'fisuser-service'
		smokeTestOperation='cicd/user/profile/11111'
		makeGetRequest("http://${serviceName}/${smokeTestOperation}")
                

		serviceName = 'fisalert-service'
		smokeTestOperation='cicd/alert'
		body = ''' { "alertType": "ACCIDENT",  "firstName": "Abdul Hameed",  "date": "11/8/2019",  "phone": "78135955",  "email": "ahameed@redhat.com",  "description": "test"} '''
		makePostRequest("http://${serviceName}/${smokeTestOperation}", body,'POST')

		serviceName = 'nodejsalert-ui'
	        makeGetRequest("http://${serviceName}:8080")
		
   	}





def makeGetRequest(url) {

	println('service...'+url);

	def get = new URL(url).openConnection();
	get.setDoOutput(true)

	get.setRequestProperty('Accept', 'application/json')
	
	def responseCode = get.getResponseCode();
	if (responseCode != 200 && responseCode != 201) {
		println('Failed. HTTP response: ' + responseCode)
		println(get.getInputStream().getText());
		assert false
	} else {
		println('test successfull!')
	       
	}
}

def makePostRequest(url, body, method) {

	System.setProperty("org.jenkinsci.plugins.permissivescriptsecurity.PermissiveWhitelist.enabled","true")


	println('service url...'+url);
	println('post body...'+body)

	def post = new URL(url).openConnection();
	post.setRequestMethod(method)
	post.setDoOutput(true)
	post.setRequestProperty('Content-Type', 'application/json')
	post.setRequestProperty('Accept', 'application/json')
	post.getOutputStream().write(body.getBytes('UTF-8'))
	def responseCode = post.getResponseCode();
	if (responseCode != 200 && responseCode != 201) {
		println('Failed. HTTP response: ' + responseCode)
		println(post.getInputStream().getText());
		assert false
	} else {
		println('test successfull!')
		println(post.getInputStream().getText());

	}
}










