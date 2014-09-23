# Build configuratie


<ul>
	<li>
		SASS
		<ul>
			<li>Autoprefixer</li>
			<li class="fragment">Stylegids & Project `dest/` folder</li>
		</ul>
	</li>
	<li class="fragment">JS
		<ul>
			<li>Comprimeren</li>
			<li class="fragment">JSHint</li>
			<li class="fragment">Overige checks</li>
		</ul>
	</li>
</ul>


```javascript
function ($scope, Module1, Service) {

}
```


```javascript
function (a, b, c) {

}
```


```javascript
['$scope', 'Module1', 'Service', function ($scope, Module1, Service) {

}]
```


```javascript
['$scope', 'Module1', 'Service', function (a, b, c) {

}]
```