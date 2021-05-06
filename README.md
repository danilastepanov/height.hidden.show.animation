# Pure JS hidden/show animation

// There is a generic div .faq container. It has a .div with a .ask class and a .answer container with text. When you click on .ask, .answer opens and close with animation //

```javascript
window.addEventListener('load', function(){

	let faq = document.querySelector('.faq');

	faq.addEventListener('click', function(e){
		if(e.target.classList.contains('ask')){
			toogleItem(e.target);
		}
	});

	function toogleItem(ask){
		let answer = ask.nextElementSibling;

		if(answer.classList.contains('open')){
			jsHeightAnimation(answer, true, function(){
				answer.classList.remove('open');
			});
		}
		else{
			answer.classList.add('open');
			jsHeightAnimation(answer);
		}
	}

});

function jsHeightAnimation(el, isReverse = false, onFinish = function(){}){
	if(el.jsAnimated === true){
		return;
	}

	el.jsAnimated = true;
	let animate = el.animate(
		[
			{ height: 0 },
			{ height: el.clientHeight + 'px' }
		], 
		{ 
			duration: 500,
			direction: isReverse ? 'reverse' : 'normal'
		}
	);

	animate.addEventListener('finish', function(){
		el.jsAnimated = false;
		onFinish();
	});
}
```

```html
<div class="faq">
            <div class="ask">Lorem ipsum dolor sit amet</div>
                <div class="answer open">
                    <p>
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit,
                        sed do eiusmod tempor incididunt ut labore et dolore
                        magna aliqua. Ut enim ad minim veniam, quis nostrud
                        exercitation ullamco laboris nisi ut aliquip ex ea
                        commodo consequat.
                    </p>
                 </div>
         </div>
```

