# jImprove
Php parser to add support for Default Parameter Values to Javascript Functions

Works with all types of values even arrays, objects and callback functions!

Lines on error reports remain coherent with the original code!

jImporve is built upon the great javascript parser jParser by Tim Whitlock: https://github.com/S3RK/jParser

I also added a function called "isDefined" to easily test if something is defined, you can change it's name or disable this functionality in jImprove.php .

Usage:
=====
	
	jImprove::compile('//some javascript code using the default parameter syntax')
	
	Returns Browser compatible javascript!
	
Examples:
=========
	
	Exemple 1: 
		
		function myfunction(a=1, b=2, c=3){
			return a + b + c;
		}
	
	Result:
	
		function myfunction(a, b, c){ if(typeof a === 'undefined'){a=1;}  if(typeof b === 'undefined'){b=2;}  if(typeof c === 'undefined'){c=3;} 
			return a + b + c;
		}
		
	
	Exemple 2: 
		
		function myfunction(a=[1,2,3]){
			//do something
		}
	
	Result:
	
		function myfunction(a){ if(typeof a === 'undefined'){a=[1,2,3];} 
			//do something
		}
	
	
	Exemple 3: 
		
		function myfunction(a, callback=function(b=1){alert(b);}){
			return callback(a);
		}
	
	Result:
	
		function myfunction(a, callback){ if(typeof callback === 'undefined'){callback=function(b){ if(typeof b === 'undefined'){b=1;} alert(b);};} 
			return callback(a);
		}
	
	
	Exemple 4: 
	
		if(!isDefined(myvar)){
			var myvar=false;
		}
	
	Result:
	
		if(!(typeof (myvar) !== 'undefined')){
			var myvar=false;
		}
		
