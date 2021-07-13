# after-scripts
# Wellcome to After Scripts!

## Loop In and Out

    loopIn() + loopOut() - value;
    
## Loop path keyframes

    if (numKeys >1 && time > key(numKeys).time){ t1 = key(1).time; t2 = key(numKeys).time; span = t2 - t1; delta = time - t2; t = delta%span; valueAtTime(t1 + t) }else value

## Loop a wiggle

> loopTime = the length in seconds you want your loop

    freq = .5;  
	amp = 20;  
	loopTime = 3;  
	t = time % loopTime;  
	wiggle1 = wiggle(freq, amp, 1, 0.5, t);  
	wiggle2 = wiggle(freq, amp, 1, 0.5, t - loopTime);  
	linear(t, 0,  loopTime, wiggle1, wiggle2)

## PosterizeTime + Wiggle

    f = 2;
	a = 10;
	posterizeTime(f);
	wiggle(f, a);

## Wiggle only One Dimension

> NOTE: Loops X dimension. For Y dimension only, change last line to  **[value[0],w[1]]**

    f = 2;
	a = 10;
	w = wiggle(f, a);  
	[w[0],value[1]]

## Wiggle between two values

    min = -10;
	max = 50;
	f = 5;  
	a = Math.abs(max-min)/2;  
	offset = (hi+lo)/2;  
	wiggle(f, a) + offset;

## Maintain scale when parented (ignore parent scale)

    s = [];  
	ps = parent.transform.scale.value;  
	for (i = 0; i < ps.length; i++){  
	s[i] = (ps[i]== 0) ? 0 : value[i]*100/ps[i];  
	}  
	s
	

> If parent has a parent

    L = thisLayer;  
	s = transform.scale.value;  
	while (L.hasParent){  
	L = L.parent;  
	for (i = 0; i < s.length; i++) s[i] *= 100/L.transform.scale.value[i]  
	}  
	s

## Ignore parent rotation

    value - parent.transform.rotation

## Control Property with Checkbox

> Apply this expression to the property you want to control (like opacity) and make sure it is referencing the correct control layer.

    thisComp.layer("Controls").effect("Control Name")("Checkbox") * value;

## Get Current Date and Format

    ```
	d = new Date(Date(0));
	// Format Settings
	divider = "/"
	yearLength = 2; // use 2 for YY, 4 for YYYY

	function padZeros(n){
	  if(n <= 9){
    return "0" + n;
	  }
	  return n
	}
	yearTrim = (yearLength===2) ? 2 : 0;
	"" + padZeros(d.getMonth()+1) + divider + padZeros(d.getDate()) + divider + 	d.getFullYear().toString().substring(yearTrim,4);
	```

## Maintain Stroke Width

    ```
	value / length(toComp([0,0]), toComp([0.7071,0.7071])) || 0.001;
	```

## Scale Layer to Certain Width

    s = 100*{{WIDTH}}/thisLayer.width;  
	[s,s]
