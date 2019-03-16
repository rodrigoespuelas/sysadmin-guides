#### Redireccionar de HTTP a HTTPS
~~~
<rewrite>
	<rules>
		<rule name="Redirect to http" enabled="true" patternSyntax="Wildcard" stopProcessing="true">
			<match url="*" negate="false" />
			<conditions logicalGrouping="MatchAny">
				<add input="{HTTPS}" pattern="off" />
			</conditions>
			<action type="Redirect" url="https://{HTTP_HOST}{REQUEST_URI}" redirectType="Found" />
		</rule>
	</rules>
</rewrite>
~~~

~~~
<configuration>
<system.webServer>
<rewrite>
    <rules>
       <rule name="HTTP to HTTPS redirect" stopProcessing="true"> 
         <match url="(.*)" /> 
         <conditions> 
           <add input="{HTTPS}" pattern="off" ignoreCase="true" />
         </conditions> 
         <action type="Redirect" redirectType="Permanent" url="https://{HTTP_HOST}/{R:1}" />
       </rule> 
    </rules>
</rewrite>
</system.webServer>
</configuration>
~~~
