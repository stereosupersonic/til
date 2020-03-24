# Bootstrap 4 Basics

cheatsheet https://hackerthemes.com/bootstrap-cheatsheet

## Grid 

* based on flexbox
* 12 column system 
* outer element is always at least one ".container" class
* don't nested ".container" class
* .row only inside .container
* .col only inside .row

### container 

```
<body>
	<div class="container bg-primary">
		<div class="row">
			<div class="col">
				<h2>.container</h2>
				<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. A accusantium aspernatur autem beatae blanditiis cumque dolorum ducimus facilis impedit in laborum magni nihil perferendis quam, quia rem sint suscipit veniam.</p>
			</div>
		</div>
	</div>
</body>
```

### fluid container 

```
<body>
	<div class="container-fluid bg-info">
		<div class="row">
			<div class="col">
				<h2>.container-fluid</h2>
				<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. A accusantium aspernatur autem beatae blanditiis cumque dolorum ducimus facilis impedit in laborum magni nihil perferendis quam, quia rem sint suscipit veniam.</p>
			</div>
		</div>
	</div>
</body>
```