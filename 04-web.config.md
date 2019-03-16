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
