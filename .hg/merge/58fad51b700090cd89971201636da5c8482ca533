/*
	Copyright (c) 2004-2011, The Dojo Foundation All Rights Reserved.
	Available via Academic Free License >= 2.1 OR the modified BSD license.
	see: http://dojotoolkit.org/license for details
*/

/*
	This is an optimized version of Dojo, built for deployment and not for
	development. To get sources and documentation, please visit:

		http://dojotoolkit.org
*/

if(!dojo._hasResource["dojo.uacss"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojo.uacss"] = true;
dojo.provide("dojo.uacss");






(function(){
	// summary:
	//		Applies pre-set CSS classes to the top-level HTML node, based on:
	// 			- browser (ex: dj_ie)
	//			- browser version (ex: dj_ie6)
	//			- box model (ex: dj_contentBox)
	//			- text direction (ex: dijitRtl)
	//
	//		In addition, browser, browser version, and box model are
	//		combined with an RTL flag when browser text is RTL.  ex: dj_ie-rtl.

	var d = dojo,
		html = d.doc.documentElement,
		ie = d.isIE,
		opera = d.isOpera,
		maj = Math.floor,
		ff = d.isFF,
		boxModel = d.boxModel.replace(/-/,''),

		classes = {
			dj_ie: ie,
			dj_ie6: maj(ie) == 6,
			dj_ie7: maj(ie) == 7,
			dj_ie8: maj(ie) == 8,
			dj_ie9: maj(ie) == 9,
			dj_quirks: d.isQuirks,
			dj_iequirks: ie && d.isQuirks,

			// NOTE: Opera not supported by dijit
			dj_opera: opera,

			dj_khtml: d.isKhtml,

			dj_webkit: d.isWebKit,
			dj_safari: d.isSafari,
			dj_chrome: d.isChrome,

			dj_gecko: d.isMozilla,
			dj_ff3: maj(ff) == 3
		}; // no dojo unsupported browsers

	classes["dj_" + boxModel] = true;

	// apply browser, browser version, and box model class names
	var classStr = "";
	for(var clz in classes){
		if(classes[clz]){
			classStr += clz + " ";
		}
	}
	html.className = d.trim(html.className + " " + classStr);

	// If RTL mode, then add dj_rtl flag plus repeat existing classes with -rtl extension.
	// We can't run the code below until the <body> tag has loaded (so we can check for dir=rtl).
	// Unshift() is to run sniff code before the parser.
	dojo._loaders.unshift(function(){
		if(!dojo._isBodyLtr()){
			var rtlClassStr = "dj_rtl dijitRtl " + classStr.replace(/ /g, "-rtl ")
			html.className = d.trim(html.className + " " + rtlClassStr);
		}
	});
})();

}

if(!dojo._hasResource["dijit._base.sniff"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dijit._base.sniff"] = true;
dojo.provide("dijit._base.sniff");




// summary:
//		Applies pre-set CSS classes to the top-level HTML node, see
//		`dojo.uacss` for details.
//
//		Simply doing a require on this module will
//		establish this CSS.  Modified version of Morris' CSS hack.

}

if(!dojo._hasResource["dojo._base.Color"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojo._base.Color"] = true;
dojo.provide("dojo._base.Color");







(function(){

	var d = dojo;

	dojo.Color = function(/*Array|String|Object*/ color){
		// summary:
		//	 	Takes a named string, hex string, array of rgb or rgba values,
		//	 	an object with r, g, b, and a properties, or another `dojo.Color` object
		//	 	and creates a new Color instance to work from.
		//
		// example:
		//		Work with a Color instance:
		//	 | var c = new dojo.Color();
		//	 | c.setColor([0,0,0]); // black
		//	 | var hex = c.toHex(); // #000000
		//
		// example:
		//		Work with a node's color:
		//	 | var color = dojo.style("someNode", "backgroundColor");
		//	 | var n = new dojo.Color(color);
		//	 | // adjust the color some
		//	 | n.r *= .5;
		//	 | console.log(n.toString()); // rgb(128, 255, 255);
		if(color){ this.setColor(color); }
	};

	// FIXME:
	// 	there's got to be a more space-efficient way to encode or discover
	// 	these!!  Use hex?
	dojo.Color.named = {
		black:      [0,0,0],
		silver:     [192,192,192],
		gray:       [128,128,128],
		white:      [255,255,255],
		maroon:		[128,0,0],
		red:        [255,0,0],
		purple:		[128,0,128],
		fuchsia:	[255,0,255],
		green:	    [0,128,0],
		lime:	    [0,255,0],
		olive:		[128,128,0],
		yellow:		[255,255,0],
		navy:       [0,0,128],
		blue:       [0,0,255],
		teal:		[0,128,128],
		aqua:		[0,255,255],
		transparent: d.config.transparentColor || [255,255,255]
	};

	dojo.extend(dojo.Color, {
		r: 255, g: 255, b: 255, a: 1,
		_set: function(r, g, b, a){
			var t = this; t.r = r; t.g = g; t.b = b; t.a = a;
		},
		setColor: function(/*Array|String|Object*/ color){
			// summary:
			//		Takes a named string, hex string, array of rgb or rgba values,
			//		an object with r, g, b, and a properties, or another `dojo.Color` object
			//		and sets this color instance to that value.
			//
			// example:
			//	|	var c = new dojo.Color(); // no color
			//	|	c.setColor("#ededed"); // greyish
			if(d.isString(color)){
				d.colorFromString(color, this);
			}else if(d.isArray(color)){
				d.colorFromArray(color, this);
			}else{
				this._set(color.r, color.g, color.b, color.a);
				if(!(color instanceof d.Color)){ this.sanitize(); }
			}
			return this;	// dojo.Color
		},
		sanitize: function(){
			// summary:
			//		Ensures the object has correct attributes
			// description:
			//		the default implementation does nothing, include dojo.colors to
			//		augment it with real checks
			return this;	// dojo.Color
		},
		toRgb: function(){
			// summary:
			//		Returns 3 component array of rgb values
			// example:
			//	|	var c = new dojo.Color("#000000");
			//	| 	console.log(c.toRgb()); // [0,0,0]
			var t = this;
			return [t.r, t.g, t.b];	// Array
		},
		toRgba: function(){
			// summary:
			//		Returns a 4 component array of rgba values from the color
			//		represented by this object.
			var t = this;
			return [t.r, t.g, t.b, t.a];	// Array
		},
		toHex: function(){
			// summary:
			//		Returns a CSS color string in hexadecimal representation
			// example:
			//	| 	console.log(new dojo.Color([0,0,0]).toHex()); // #000000
			var arr = d.map(["r", "g", "b"], function(x){
				var s = this[x].toString(16);
				return s.length < 2 ? "0" + s : s;
			}, this);
			return "#" + arr.join("");	// String
		},
		toCss: function(/*Boolean?*/ includeAlpha){
			// summary:
			//		Returns a css color string in rgb(a) representation
			// example:
			//	|	var c = new dojo.Color("#FFF").toCss();
			//	|	console.log(c); // rgb('255','255','255')
			var t = this, rgb = t.r + ", " + t.g + ", " + t.b;
			return (includeAlpha ? "rgba(" + rgb + ", " + t.a : "rgb(" + rgb) + ")";	// String
		},
		toString: function(){
			// summary:
			//		Returns a visual representation of the color
			return this.toCss(true); // String
		}
	});

	dojo.blendColors = function(
		/*dojo.Color*/ start,
		/*dojo.Color*/ end,
		/*Number*/ weight,
		/*dojo.Color?*/ obj
	){
		// summary:
		//		Blend colors end and start with weight from 0 to 1, 0.5 being a 50/50 blend,
		//		can reuse a previously allocated dojo.Color object for the result
		var t = obj || new d.Color();
		d.forEach(["r", "g", "b", "a"], function(x){
			t[x] = start[x] + (end[x] - start[x]) * weight;
			if(x != "a"){ t[x] = Math.round(t[x]); }
		});
		return t.sanitize();	// dojo.Color
	};

	dojo.colorFromRgb = function(/*String*/ color, /*dojo.Color?*/ obj){
		// summary:
		//		Returns a `dojo.Color` instance from a string of the form
		//		"rgb(...)" or "rgba(...)". Optionally accepts a `dojo.Color`
		//		object to update with the parsed value and return instead of
		//		creating a new object.
		// returns:
		//		A dojo.Color object. If obj is passed, it will be the return value.
		var m = color.toLowerCase().match(/^rgba?\(([\s\.,0-9]+)\)/);
		return m && dojo.colorFromArray(m[1].split(/\s*,\s*/), obj);	// dojo.Color
	};

	dojo.colorFromHex = function(/*String*/ color, /*dojo.Color?*/ obj){
		// summary:
		//		Converts a hex string with a '#' prefix to a color object.
		//		Supports 12-bit #rgb shorthand. Optionally accepts a
		//		`dojo.Color` object to update with the parsed value.
		//
		// returns:
		//		A dojo.Color object. If obj is passed, it will be the return value.
		//
		// example:
		//	 | var thing = dojo.colorFromHex("#ededed"); // grey, longhand
		//
		// example:
		//	| var thing = dojo.colorFromHex("#000"); // black, shorthand
		var t = obj || new d.Color(),
			bits = (color.length == 4) ? 4 : 8,
			mask = (1 << bits) - 1;
		color = Number("0x" + color.substr(1));
		if(isNaN(color)){
			return null; // dojo.Color
		}
		d.forEach(["b", "g", "r"], function(x){
			var c = color & mask;
			color >>= bits;
			t[x] = bits == 4 ? 17 * c : c;
		});
		t.a = 1;
		return t;	// dojo.Color
	};

	dojo.colorFromArray = function(/*Array*/ a, /*dojo.Color?*/ obj){
		// summary:
		//		Builds a `dojo.Color` from a 3 or 4 element array, mapping each
		//		element in sequence to the rgb(a) values of the color.
		// example:
		//		| var myColor = dojo.colorFromArray([237,237,237,0.5]); // grey, 50% alpha
		// returns:
		//		A dojo.Color object. If obj is passed, it will be the return value.
		var t = obj || new d.Color();
		t._set(Number(a[0]), Number(a[1]), Number(a[2]), Number(a[3]));
		if(isNaN(t.a)){ t.a = 1; }
		return t.sanitize();	// dojo.Color
	};

	dojo.colorFromString = function(/*String*/ str, /*dojo.Color?*/ obj){
		// summary:
		//		Parses `str` for a color value. Accepts hex, rgb, and rgba
		//		style color values.
		// description:
		//		Acceptable input values for str may include arrays of any form
		//		accepted by dojo.colorFromArray, hex strings such as "#aaaaaa", or
		//		rgb or rgba strings such as "rgb(133, 200, 16)" or "rgba(10, 10,
		//		10, 50)"
		// returns:
		//		A dojo.Color object. If obj is passed, it will be the return value.
		var a = d.Color.named[str];
		return a && d.colorFromArray(a, obj) || d.colorFromRgb(str, obj) || d.colorFromHex(str, obj);
	};
})();

}

if(!dojo._hasResource["dojo._base.fx"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojo._base.fx"] = true;
dojo.provide("dojo._base.fx");












/*
	Animation loosely package based on Dan Pupius' work, contributed under CLA:
		http://pupius.co.uk/js/Toolkit.Drawing.js
*/
(function(){
	var d = dojo;
	var _mixin = d._mixin;

	dojo._Line = function(/*int*/ start, /*int*/ end){
		//	summary:
		//		dojo._Line is the object used to generate values from a start value
		//		to an end value
		//	start: int
		//		Beginning value for range
		//	end: int
		//		Ending value for range
		this.start = start;
		this.end = end;
	};

	dojo._Line.prototype.getValue = function(/*float*/ n){
		//	summary: Returns the point on the line
		//	n: a floating point number greater than 0 and less than 1
		return ((this.end - this.start) * n) + this.start; // Decimal
	};

	dojo.Animation = function(args){
		//	summary:
		//		A generic animation class that fires callbacks into its handlers
		//		object at various states.
		//	description:
		//		A generic animation class that fires callbacks into its handlers
		//		object at various states. Nearly all dojo animation functions
		//		return an instance of this method, usually without calling the
		//		.play() method beforehand. Therefore, you will likely need to
		//		call .play() on instances of `dojo.Animation` when one is
		//		returned.
		// args: Object
		//		The 'magic argument', mixing all the properties into this
		//		animation instance.

		_mixin(this, args);
		if(d.isArray(this.curve)){
			this.curve = new d._Line(this.curve[0], this.curve[1]);
		}

	};

	// Alias to drop come 2.0:
	d._Animation = d.Animation;

	d.extend(dojo.Animation, {
		// duration: Integer
		//		The time in milliseonds the animation will take to run
		duration: 350,

	/*=====
		// curve: dojo._Line|Array
		//		A two element array of start and end values, or a `dojo._Line` instance to be
		//		used in the Animation.
		curve: null,

		// easing: Function?
		//		A Function to adjust the acceleration (or deceleration) of the progress
		//		across a dojo._Line
		easing: null,
	=====*/

		// repeat: Integer?
		//		The number of times to loop the animation
		repeat: 0,

		// rate: Integer?
		//		the time in milliseconds to wait before advancing to next frame
		//		(used as a fps timer: 1000/rate = fps)
		rate: 20 /* 50 fps */,

	/*=====
		// delay: Integer?
		//		The time in milliseconds to wait before starting animation after it
		//		has been .play()'ed
		delay: null,

		// beforeBegin: Event?
		//		Synthetic event fired before a dojo.Animation begins playing (synchronous)
		beforeBegin: null,

		// onBegin: Event?
		//		Synthetic event fired as a dojo.Animation begins playing (useful?)
		onBegin: null,

		// onAnimate: Event?
		//		Synthetic event fired at each interval of a `dojo.Animation`
		onAnimate: null,

		// onEnd: Event?
		//		Synthetic event fired after the final frame of a `dojo.Animation`
		onEnd: null,

		// onPlay: Event?
		//		Synthetic event fired any time a `dojo.Animation` is play()'ed
		onPlay: null,

		// onPause: Event?
		//		Synthetic event fired when a `dojo.Animation` is paused
		onPause: null,

		// onStop: Event
		//		Synthetic event fires when a `dojo.Animation` is stopped
		onStop: null,

	=====*/

		_percent: 0,
		_startRepeatCount: 0,

		_getStep: function(){
			var _p = this._percent,
				_e = this.easing
			;
			return _e ? _e(_p) : _p;
		},
		_fire: function(/*Event*/ evt, /*Array?*/ args){
			//	summary:
			//		Convenience function.  Fire event "evt" and pass it the
			//		arguments specified in "args".
			//	description:
			//		Convenience function.  Fire event "evt" and pass it the
			//		arguments specified in "args".
			//		Fires the callback in the scope of the `dojo.Animation`
			//		instance.
			//	evt:
			//		The event to fire.
			//	args:
			//		The arguments to pass to the event.
			var a = args||[];
			if(this[evt]){
				if(d.config.debugAtAllCosts){
					this[evt].apply(this, a);
				}else{
					try{
						this[evt].apply(this, a);
					}catch(e){
						// squelch and log because we shouldn't allow exceptions in
						// synthetic event handlers to cause the internal timer to run
						// amuck, potentially pegging the CPU. I'm not a fan of this
						// squelch, but hopefully logging will make it clear what's
						// going on
						console.error("exception in animation handler for:", evt);
						console.error(e);
					}
				}
			}
			return this; // dojo.Animation
		},

		play: function(/*int?*/ delay, /*Boolean?*/ gotoStart){
			// summary:
			//		Start the animation.
			// delay:
			//		How many milliseconds to delay before starting.
			// gotoStart:
			//		If true, starts the animation from the beginning; otherwise,
			//		starts it from its current position.
			// returns: dojo.Animation
			//		The instance to allow chaining.

			var _t = this;
			if(_t._delayTimer){ _t._clearTimer(); }
			if(gotoStart){
				_t._stopTimer();
				_t._active = _t._paused = false;
				_t._percent = 0;
			}else if(_t._active && !_t._paused){
				return _t;
			}

			_t._fire("beforeBegin", [_t.node]);

			var de = delay || _t.delay,
				_p = dojo.hitch(_t, "_play", gotoStart);

			if(de > 0){
				_t._delayTimer = setTimeout(_p, de);
				return _t;
			}
			_p();
			return _t;
		},

		_play: function(gotoStart){
			var _t = this;
			if(_t._delayTimer){ _t._clearTimer(); }
			_t._startTime = new Date().valueOf();
			if(_t._paused){
				_t._startTime -= _t.duration * _t._percent;
			}

			_t._active = true;
			_t._paused = false;
			var value = _t.curve.getValue(_t._getStep());
			if(!_t._percent){
				if(!_t._startRepeatCount){
					_t._startRepeatCount = _t.repeat;
				}
				_t._fire("onBegin", [value]);
			}

			_t._fire("onPlay", [value]);

			_t._cycle();
			return _t; // dojo.Animation
		},

		pause: function(){
			// summary: Pauses a running animation.
			var _t = this;
			if(_t._delayTimer){ _t._clearTimer(); }
			_t._stopTimer();
			if(!_t._active){ return _t; /*dojo.Animation*/ }
			_t._paused = true;
			_t._fire("onPause", [_t.curve.getValue(_t._getStep())]);
			return _t; // dojo.Animation
		},

		gotoPercent: function(/*Decimal*/ percent, /*Boolean?*/ andPlay){
			//	summary:
			//		Sets the progress of the animation.
			//	percent:
			//		A percentage in decimal notation (between and including 0.0 and 1.0).
			//	andPlay:
			//		If true, play the animation after setting the progress.
			var _t = this;
			_t._stopTimer();
			_t._active = _t._paused = true;
			_t._percent = percent;
			if(andPlay){ _t.play(); }
			return _t; // dojo.Animation
		},

		stop: function(/*boolean?*/ gotoEnd){
			// summary: Stops a running animation.
			// gotoEnd: If true, the animation will end.
			var _t = this;
			if(_t._delayTimer){ _t._clearTimer(); }
			if(!_t._timer){ return _t; /* dojo.Animation */ }
			_t._stopTimer();
			if(gotoEnd){
				_t._percent = 1;
			}
			_t._fire("onStop", [_t.curve.getValue(_t._getStep())]);
			_t._active = _t._paused = false;
			return _t; // dojo.Animation
		},

		status: function(){
			// summary:
			//		Returns a string token representation of the status of
			//		the animation, one of: "paused", "playing", "stopped"
			if(this._active){
				return this._paused ? "paused" : "playing"; // String
			}
			return "stopped"; // String
		},

		_cycle: function(){
			var _t = this;
			if(_t._active){
				var curr = new Date().valueOf();
				var step = (curr - _t._startTime) / (_t.duration);

				if(step >= 1){
					step = 1;
				}
				_t._percent = step;

				// Perform easing
				if(_t.easing){
					step = _t.easing(step);
				}

				_t._fire("onAnimate", [_t.curve.getValue(step)]);

				if(_t._percent < 1){
					_t._startTimer();
				}else{
					_t._active = false;

					if(_t.repeat > 0){
						_t.repeat--;
						_t.play(null, true);
					}else if(_t.repeat == -1){
						_t.play(null, true);
					}else{
						if(_t._startRepeatCount){
							_t.repeat = _t._startRepeatCount;
							_t._startRepeatCount = 0;
						}
					}
					_t._percent = 0;
					_t._fire("onEnd", [_t.node]);
					!_t.repeat && _t._stopTimer();
				}
			}
			return _t; // dojo.Animation
		},

		_clearTimer: function(){
			// summary: Clear the play delay timer
			clearTimeout(this._delayTimer);
			delete this._delayTimer;
		}

	});

	// the local timer, stubbed into all Animation instances
	var ctr = 0,
		timer = null,
		runner = {
			run: function(){}
		};

	d.extend(d.Animation, {

		_startTimer: function(){
			if(!this._timer){
				this._timer = d.connect(runner, "run", this, "_cycle");
				ctr++;
			}
			if(!timer){
				timer = setInterval(d.hitch(runner, "run"), this.rate);
			}
		},

		_stopTimer: function(){
			if(this._timer){
				d.disconnect(this._timer);
				this._timer = null;
				ctr--;
			}
			if(ctr <= 0){
				clearInterval(timer);
				timer = null;
				ctr = 0;
			}
		}

	});

	var _makeFadeable =
				d.isIE ? function(node){
			// only set the zoom if the "tickle" value would be the same as the
			// default
			var ns = node.style;
			// don't set the width to auto if it didn't already cascade that way.
			// We don't want to f anyones designs
			if(!ns.width.length && d.style(node, "width") == "auto"){
				ns.width = "auto";
			}
		} :
				function(){};

	dojo._fade = function(/*Object*/ args){
		//	summary:
		//		Returns an animation that will fade the node defined by
		//		args.node from the start to end values passed (args.start
		//		args.end) (end is mandatory, start is optional)

		args.node = d.byId(args.node);
		var fArgs = _mixin({ properties: {} }, args),
			props = (fArgs.properties.opacity = {});

		props.start = !("start" in fArgs) ?
			function(){
				return +d.style(fArgs.node, "opacity")||0;
			} : fArgs.start;
		props.end = fArgs.end;

		var anim = d.animateProperty(fArgs);
		d.connect(anim, "beforeBegin", d.partial(_makeFadeable, fArgs.node));

		return anim; // dojo.Animation
	};

	/*=====
	dojo.__FadeArgs = function(node, duration, easing){
		//	node: DOMNode|String
		//		The node referenced in the animation
		//	duration: Integer?
		//		Duration of the animation in milliseconds.
		//	easing: Function?
		//		An easing function.
		this.node = node;
		this.duration = duration;
		this.easing = easing;
	}
	=====*/

	dojo.fadeIn = function(/*dojo.__FadeArgs*/ args){
		// summary:
		//		Returns an animation that will fade node defined in 'args' from
		//		its current opacity to fully opaque.
		return d._fade(_mixin({ end: 1 }, args)); // dojo.Animation
	};

	dojo.fadeOut = function(/*dojo.__FadeArgs*/  args){
		// summary:
		//		Returns an animation that will fade node defined in 'args'
		//		from its current opacity to fully transparent.
		return d._fade(_mixin({ end: 0 }, args)); // dojo.Animation
	};

	dojo._defaultEasing = function(/*Decimal?*/ n){
		// summary: The default easing function for dojo.Animation(s)
		return 0.5 + ((Math.sin((n + 1.5) * Math.PI)) / 2);
	};

	var PropLine = function(properties){
		// PropLine is an internal class which is used to model the values of
		// an a group of CSS properties across an animation lifecycle. In
		// particular, the "getValue" function handles getting interpolated
		// values between start and end for a particular CSS value.
		this._properties = properties;
		for(var p in properties){
			var prop = properties[p];
			if(prop.start instanceof d.Color){
				// create a reusable temp color object to keep intermediate results
				prop.tempColor = new d.Color();
			}
		}
	};

	PropLine.prototype.getValue = function(r){
		var ret = {};
		for(var p in this._properties){
			var prop = this._properties[p],
				start = prop.start;
			if(start instanceof d.Color){
				ret[p] = d.blendColors(start, prop.end, r, prop.tempColor).toCss();
			}else if(!d.isArray(start)){
				ret[p] = ((prop.end - start) * r) + start + (p != "opacity" ? prop.units || "px" : 0);
			}
		}
		return ret;
	};

	/*=====
	dojo.declare("dojo.__AnimArgs", [dojo.__FadeArgs], {
		// Properties: Object?
		//	A hash map of style properties to Objects describing the transition,
		//	such as the properties of dojo._Line with an additional 'units' property
		properties: {}

		//TODOC: add event callbacks
	});
	=====*/

	dojo.animateProperty = function(/*dojo.__AnimArgs*/ args){
		// summary:
		//		Returns an animation that will transition the properties of
		//		node defined in `args` depending how they are defined in
		//		`args.properties`
		//
		// description:
		//		`dojo.animateProperty` is the foundation of most `dojo.fx`
		//		animations. It takes an object of "properties" corresponding to
		//		style properties, and animates them in parallel over a set
		//		duration.
		//
		// example:
		//		A simple animation that changes the width of the specified node.
		//	|	dojo.animateProperty({
		//	|		node: "nodeId",
		//	|		properties: { width: 400 },
		//	|	}).play();
		//		Dojo figures out the start value for the width and converts the
		//		integer specified for the width to the more expressive but
		//		verbose form `{ width: { end: '400', units: 'px' } }` which you
		//		can also specify directly. Defaults to 'px' if ommitted.
		//
		// example:
		//		Animate width, height, and padding over 2 seconds... the
		//		pedantic way:
		//	|	dojo.animateProperty({ node: node, duration:2000,
		//	|		properties: {
		//	|			width: { start: '200', end: '400', units:"px" },
		//	|			height: { start:'200', end: '400', units:"px" },
		//	|			paddingTop: { start:'5', end:'50', units:"px" }
		//	|		}
		//	|	}).play();
		//		Note 'paddingTop' is used over 'padding-top'. Multi-name CSS properties
		//		are written using "mixed case", as the hyphen is illegal as an object key.
		//
		// example:
		//		Plug in a different easing function and register a callback for
		//		when the animation ends. Easing functions accept values between
		//		zero and one and return a value on that basis. In this case, an
		//		exponential-in curve.
		//	|	dojo.animateProperty({
		//	|		node: "nodeId",
		//	|		// dojo figures out the start value
		//	|		properties: { width: { end: 400 } },
		//	|		easing: function(n){
		//	|			return (n==0) ? 0 : Math.pow(2, 10 * (n - 1));
		//	|		},
		//	|		onEnd: function(node){
		//	|			// called when the animation finishes. The animation
		//	|			// target is passed to this function
		//	|		}
		//	|	}).play(500); // delay playing half a second
		//
		// example:
		//		Like all `dojo.Animation`s, animateProperty returns a handle to the
		//		Animation instance, which fires the events common to Dojo FX. Use `dojo.connect`
		//		to access these events outside of the Animation definiton:
		//	|	var anim = dojo.animateProperty({
		//	|		node:"someId",
		//	|		properties:{
		//	|			width:400, height:500
		//	|		}
		//	|	});
		//	|	dojo.connect(anim,"onEnd", function(){
		//	|		console.log("animation ended");
		//	|	});
		//	|	// play the animation now:
		//	|	anim.play();
		//
		// example:
		//		Each property can be a function whose return value is substituted along.
		//		Additionally, each measurement (eg: start, end) can be a function. The node
		//		reference is passed direcly to callbacks.
		//	|	dojo.animateProperty({
		//	|		node:"mine",
		//	|		properties:{
		//	|			height:function(node){
		//	|				// shrink this node by 50%
		//	|				return dojo.position(node).h / 2
		//	|			},
		//	|			width:{
		//	|				start:function(node){ return 100; },
		//	|				end:function(node){ return 200; }
		//	|			}
		//	|		}
		//	|	}).play();
		//

		var n = args.node = d.byId(args.node);
		if(!args.easing){ args.easing = d._defaultEasing; }

		var anim = new d.Animation(args);
		d.connect(anim, "beforeBegin", anim, function(){
			var pm = {};
			for(var p in this.properties){
				// Make shallow copy of properties into pm because we overwrite
				// some values below. In particular if start/end are functions
				// we don't want to overwrite them or the functions won't be
				// called if the animation is reused.
				if(p == "width" || p == "height"){
					this.node.display = "block";
				}
				var prop = this.properties[p];
				if(d.isFunction(prop)){
					prop = prop(n);
				}
				prop = pm[p] = _mixin({}, (d.isObject(prop) ? prop: { end: prop }));

				if(d.isFunction(prop.start)){
					prop.start = prop.start(n);
				}
				if(d.isFunction(prop.end)){
					prop.end = prop.end(n);
				}
				var isColor = (p.toLowerCase().indexOf("color") >= 0);
				function getStyle(node, p){
					// dojo.style(node, "height") can return "auto" or "" on IE; this is more reliable:
					var v = { height: node.offsetHeight, width: node.offsetWidth }[p];
					if(v !== undefined){ return v; }
					v = d.style(node, p);
					return (p == "opacity") ? +v : (isColor ? v : parseFloat(v));
				}
				if(!("end" in prop)){
					prop.end = getStyle(n, p);
				}else if(!("start" in prop)){
					prop.start = getStyle(n, p);
				}

				if(isColor){
					prop.start = new d.Color(prop.start);
					prop.end = new d.Color(prop.end);
				}else{
					prop.start = (p == "opacity") ? +prop.start : parseFloat(prop.start);
				}
			}
			this.curve = new PropLine(pm);
		});
		d.connect(anim, "onAnimate", d.hitch(d, "style", anim.node));
		return anim; // dojo.Animation
	};

	dojo.anim = function(	/*DOMNode|String*/	node,
							/*Object*/			properties,
							/*Integer?*/		duration,
							/*Function?*/		easing,
							/*Function?*/		onEnd,
							/*Integer?*/		delay){
		//	summary:
		//		A simpler interface to `dojo.animateProperty()`, also returns
		//		an instance of `dojo.Animation` but begins the animation
		//		immediately, unlike nearly every other Dojo animation API.
		//	description:
		//		`dojo.anim` is a simpler (but somewhat less powerful) version
		//		of `dojo.animateProperty`.  It uses defaults for many basic properties
		//		and allows for positional parameters to be used in place of the
		//		packed "property bag" which is used for other Dojo animation
		//		methods.
		//
		//		The `dojo.Animation` object returned from `dojo.anim` will be
		//		already playing when it is returned from this function, so
		//		calling play() on it again is (usually) a no-op.
		//	node:
		//		a DOM node or the id of a node to animate CSS properties on
		//	duration:
		//		The number of milliseconds over which the animation
		//		should run. Defaults to the global animation default duration
		//		(350ms).
		//	easing:
		//		An easing function over which to calculate acceleration
		//		and deceleration of the animation through its duration.
		//		A default easing algorithm is provided, but you may
		//		plug in any you wish. A large selection of easing algorithms
		//		are available in `dojo.fx.easing`.
		//	onEnd:
		//		A function to be called when the animation finishes
		//		running.
		//	delay:
		//		The number of milliseconds to delay beginning the
		//		animation by. The default is 0.
		//	example:
		//		Fade out a node
		//	|	dojo.anim("id", { opacity: 0 });
		//	example:
		//		Fade out a node over a full second
		//	|	dojo.anim("id", { opacity: 0 }, 1000);
		return d.animateProperty({ // dojo.Animation
			node: node,
			duration: duration || d.Animation.prototype.duration,
			properties: properties,
			easing: easing,
			onEnd: onEnd
		}).play(delay || 0);
	};
})();

}

if(!dojo._hasResource["dojo.fx.Toggler"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojo.fx.Toggler"] = true;
dojo.provide("dojo.fx.Toggler");







dojo.declare("dojo.fx.Toggler", null, {
	// summary:
	//		A simple `dojo.Animation` toggler API.
	//
	// description:
	//		class constructor for an animation toggler. It accepts a packed
	//		set of arguments about what type of animation to use in each
	//		direction, duration, etc. All available members are mixed into
	//		these animations from the constructor (for example, `node`,
	//		`showDuration`, `hideDuration`).
	//
	// example:
	//	|	var t = new dojo.fx.Toggler({
	//	|		node: "nodeId",
	//	|		showDuration: 500,
	//	|		// hideDuration will default to "200"
	//	|		showFunc: dojo.fx.wipeIn,
	//	|		// hideFunc will default to "fadeOut"
	//	|	});
	//	|	t.show(100); // delay showing for 100ms
	//	|	// ...time passes...
	//	|	t.hide();

	// node: DomNode
	//		the node to target for the showing and hiding animations
	node: null,

	// showFunc: Function
	//		The function that returns the `dojo.Animation` to show the node
	showFunc: dojo.fadeIn,

	// hideFunc: Function
	//		The function that returns the `dojo.Animation` to hide the node
	hideFunc: dojo.fadeOut,

	// showDuration:
	//		Time in milliseconds to run the show Animation
	showDuration: 200,

	// hideDuration:
	//		Time in milliseconds to run the hide Animation
	hideDuration: 200,

	// FIXME: need a policy for where the toggler should "be" the next
	// time show/hide are called if we're stopped somewhere in the
	// middle.
	// FIXME: also would be nice to specify individual showArgs/hideArgs mixed into
	// each animation individually.
	// FIXME: also would be nice to have events from the animations exposed/bridged

	/*=====
	_showArgs: null,
	_showAnim: null,

	_hideArgs: null,
	_hideAnim: null,

	_isShowing: false,
	_isHiding: false,
	=====*/

	constructor: function(args){
		var _t = this;

		dojo.mixin(_t, args);
		_t.node = args.node;
		_t._showArgs = dojo.mixin({}, args);
		_t._showArgs.node = _t.node;
		_t._showArgs.duration = _t.showDuration;
		_t.showAnim = _t.showFunc(_t._showArgs);

		_t._hideArgs = dojo.mixin({}, args);
		_t._hideArgs.node = _t.node;
		_t._hideArgs.duration = _t.hideDuration;
		_t.hideAnim = _t.hideFunc(_t._hideArgs);

		dojo.connect(_t.showAnim, "beforeBegin", dojo.hitch(_t.hideAnim, "stop", true));
		dojo.connect(_t.hideAnim, "beforeBegin", dojo.hitch(_t.showAnim, "stop", true));
	},

	show: function(delay){
		// summary: Toggle the node to showing
		// delay: Integer?
		//		Ammount of time to stall playing the show animation
		return this.showAnim.play(delay || 0);
	},

	hide: function(delay){
		// summary: Toggle the node to hidden
		// delay: Integer?
		//		Ammount of time to stall playing the hide animation
		return this.hideAnim.play(delay || 0);
	}
});

}

if(!dojo._hasResource["dojo.fx"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojo.fx"] = true;
dojo.provide("dojo.fx");









/*=====
dojo.fx = {
	// summary: Effects library on top of Base animations
};
=====*/
(function(){
	
	var d = dojo,
		_baseObj = {
			_fire: function(evt, args){
				if(this[evt]){
					this[evt].apply(this, args||[]);
				}
				return this;
			}
		};

	var _chain = function(animations){
		this._index = -1;
		this._animations = animations||[];
		this._current = this._onAnimateCtx = this._onEndCtx = null;

		this.duration = 0;
		d.forEach(this._animations, function(a){
			this.duration += a.duration;
			if(a.delay){ this.duration += a.delay; }
		}, this);
	};
	d.extend(_chain, {
		_onAnimate: function(){
			this._fire("onAnimate", arguments);
		},
		_onEnd: function(){
			d.disconnect(this._onAnimateCtx);
			d.disconnect(this._onEndCtx);
			this._onAnimateCtx = this._onEndCtx = null;
			if(this._index + 1 == this._animations.length){
				this._fire("onEnd");
			}else{
				// switch animations
				this._current = this._animations[++this._index];
				this._onAnimateCtx = d.connect(this._current, "onAnimate", this, "_onAnimate");
				this._onEndCtx = d.connect(this._current, "onEnd", this, "_onEnd");
				this._current.play(0, true);
			}
		},
		play: function(/*int?*/ delay, /*Boolean?*/ gotoStart){
			if(!this._current){ this._current = this._animations[this._index = 0]; }
			if(!gotoStart && this._current.status() == "playing"){ return this; }
			var beforeBegin = d.connect(this._current, "beforeBegin", this, function(){
					this._fire("beforeBegin");
				}),
				onBegin = d.connect(this._current, "onBegin", this, function(arg){
					this._fire("onBegin", arguments);
				}),
				onPlay = d.connect(this._current, "onPlay", this, function(arg){
					this._fire("onPlay", arguments);
					d.disconnect(beforeBegin);
					d.disconnect(onBegin);
					d.disconnect(onPlay);
				});
			if(this._onAnimateCtx){
				d.disconnect(this._onAnimateCtx);
			}
			this._onAnimateCtx = d.connect(this._current, "onAnimate", this, "_onAnimate");
			if(this._onEndCtx){
				d.disconnect(this._onEndCtx);
			}
			this._onEndCtx = d.connect(this._current, "onEnd", this, "_onEnd");
			this._current.play.apply(this._current, arguments);
			return this;
		},
		pause: function(){
			if(this._current){
				var e = d.connect(this._current, "onPause", this, function(arg){
						this._fire("onPause", arguments);
						d.disconnect(e);
					});
				this._current.pause();
			}
			return this;
		},
		gotoPercent: function(/*Decimal*/percent, /*Boolean?*/ andPlay){
			this.pause();
			var offset = this.duration * percent;
			this._current = null;
			d.some(this._animations, function(a){
				if(a.duration <= offset){
					this._current = a;
					return true;
				}
				offset -= a.duration;
				return false;
			});
			if(this._current){
				this._current.gotoPercent(offset / this._current.duration, andPlay);
			}
			return this;
		},
		stop: function(/*boolean?*/ gotoEnd){
			if(this._current){
				if(gotoEnd){
					for(; this._index + 1 < this._animations.length; ++this._index){
						this._animations[this._index].stop(true);
					}
					this._current = this._animations[this._index];
				}
				var e = d.connect(this._current, "onStop", this, function(arg){
						this._fire("onStop", arguments);
						d.disconnect(e);
					});
				this._current.stop();
			}
			return this;
		},
		status: function(){
			return this._current ? this._current.status() : "stopped";
		},
		destroy: function(){
			if(this._onAnimateCtx){ d.disconnect(this._onAnimateCtx); }
			if(this._onEndCtx){ d.disconnect(this._onEndCtx); }
		}
	});
	d.extend(_chain, _baseObj);

	dojo.fx.chain = function(/*dojo.Animation[]*/ animations){
		// summary:
		//		Chain a list of `dojo.Animation`s to run in sequence
		//
		// description:
		//		Return a `dojo.Animation` which will play all passed
		//		`dojo.Animation` instances in sequence, firing its own
		//		synthesized events simulating a single animation. (eg:
		//		onEnd of this animation means the end of the chain,
		//		not the individual animations within)
		//
		// example:
		//	Once `node` is faded out, fade in `otherNode`
		//	|	dojo.fx.chain([
		//	|		dojo.fadeIn({ node:node }),
		//	|		dojo.fadeOut({ node:otherNode })
		//	|	]).play();
		//
		return new _chain(animations) // dojo.Animation
	};

	var _combine = function(animations){
		this._animations = animations||[];
		this._connects = [];
		this._finished = 0;

		this.duration = 0;
		d.forEach(animations, function(a){
			var duration = a.duration;
			if(a.delay){ duration += a.delay; }
			if(this.duration < duration){ this.duration = duration; }
			this._connects.push(d.connect(a, "onEnd", this, "_onEnd"));
		}, this);
		
		this._pseudoAnimation = new d.Animation({curve: [0, 1], duration: this.duration});
		var self = this;
		d.forEach(["beforeBegin", "onBegin", "onPlay", "onAnimate", "onPause", "onStop", "onEnd"],
			function(evt){
				self._connects.push(d.connect(self._pseudoAnimation, evt,
					function(){ self._fire(evt, arguments); }
				));
			}
		);
	};
	d.extend(_combine, {
		_doAction: function(action, args){
			d.forEach(this._animations, function(a){
				a[action].apply(a, args);
			});
			return this;
		},
		_onEnd: function(){
			if(++this._finished > this._animations.length){
				this._fire("onEnd");
			}
		},
		_call: function(action, args){
			var t = this._pseudoAnimation;
			t[action].apply(t, args);
		},
		play: function(/*int?*/ delay, /*Boolean?*/ gotoStart){
			this._finished = 0;
			this._doAction("play", arguments);
			this._call("play", arguments);
			return this;
		},
		pause: function(){
			this._doAction("pause", arguments);
			this._call("pause", arguments);
			return this;
		},
		gotoPercent: function(/*Decimal*/percent, /*Boolean?*/ andPlay){
			var ms = this.duration * percent;
			d.forEach(this._animations, function(a){
				a.gotoPercent(a.duration < ms ? 1 : (ms / a.duration), andPlay);
			});
			this._call("gotoPercent", arguments);
			return this;
		},
		stop: function(/*boolean?*/ gotoEnd){
			this._doAction("stop", arguments);
			this._call("stop", arguments);
			return this;
		},
		status: function(){
			return this._pseudoAnimation.status();
		},
		destroy: function(){
			d.forEach(this._connects, dojo.disconnect);
		}
	});
	d.extend(_combine, _baseObj);

	dojo.fx.combine = function(/*dojo.Animation[]*/ animations){
		// summary:
		//		Combine a list of `dojo.Animation`s to run in parallel
		//
		// description:
		//		Combine an array of `dojo.Animation`s to run in parallel,
		//		providing a new `dojo.Animation` instance encompasing each
		//		animation, firing standard animation events.
		//
		// example:
		//	Fade out `node` while fading in `otherNode` simultaneously
		//	|	dojo.fx.combine([
		//	|		dojo.fadeIn({ node:node }),
		//	|		dojo.fadeOut({ node:otherNode })
		//	|	]).play();
		//
		// example:
		//	When the longest animation ends, execute a function:
		//	|	var anim = dojo.fx.combine([
		//	|		dojo.fadeIn({ node: n, duration:700 }),
		//	|		dojo.fadeOut({ node: otherNode, duration: 300 })
		//	|	]);
		//	|	dojo.connect(anim, "onEnd", function(){
		//	|		// overall animation is done.
		//	|	});
		//	|	anim.play(); // play the animation
		//
		return new _combine(animations); // dojo.Animation
	};

	dojo.fx.wipeIn = function(/*Object*/ args){
		// summary:
		//		Expand a node to it's natural height.
		//
		// description:
		//		Returns an animation that will expand the
		//		node defined in 'args' object from it's current height to
		//		it's natural height (with no scrollbar).
		//		Node must have no margin/border/padding.
		//
		// args: Object
		//		A hash-map of standard `dojo.Animation` constructor properties
		//		(such as easing: node: duration: and so on)
		//
		// example:
		//	|	dojo.fx.wipeIn({
		//	|		node:"someId"
		//	|	}).play()
		var node = args.node = d.byId(args.node), s = node.style, o;

		var anim = d.animateProperty(d.mixin({
			properties: {
				height: {
					// wrapped in functions so we wait till the last second to query (in case value has changed)
					start: function(){
						// start at current [computed] height, but use 1px rather than 0
						// because 0 causes IE to display the whole panel
						o = s.overflow;
						s.overflow = "hidden";
						if(s.visibility == "hidden" || s.display == "none"){
							s.height = "1px";
							s.display = "";
							s.visibility = "";
							return 1;
						}else{
							var height = d.style(node, "height");
							return Math.max(height, 1);
						}
					},
					end: function(){
						return node.scrollHeight;
					}
				}
			}
		}, args));

		d.connect(anim, "onEnd", function(){
			s.height = "auto";
			s.overflow = o;
		});

		return anim; // dojo.Animation
	};

	dojo.fx.wipeOut = function(/*Object*/ args){
		// summary:
		//		Shrink a node to nothing and hide it.
		//
		// description:
		//		Returns an animation that will shrink node defined in "args"
		//		from it's current height to 1px, and then hide it.
		//
		// args: Object
		//		A hash-map of standard `dojo.Animation` constructor properties
		//		(such as easing: node: duration: and so on)
		//
		// example:
		//	|	dojo.fx.wipeOut({ node:"someId" }).play()
		
		var node = args.node = d.byId(args.node), s = node.style, o;
		
		var anim = d.animateProperty(d.mixin({
			properties: {
				height: {
					end: 1 // 0 causes IE to display the whole panel
				}
			}
		}, args));

		d.connect(anim, "beforeBegin", function(){
			o = s.overflow;
			s.overflow = "hidden";
			s.display = "";
		});
		d.connect(anim, "onEnd", function(){
			s.overflow = o;
			s.height = "auto";
			s.display = "none";
		});

		return anim; // dojo.Animation
	};

	dojo.fx.slideTo = function(/*Object*/ args){
		// summary:
		//		Slide a node to a new top/left position
		//
		// description:
		//		Returns an animation that will slide "node"
		//		defined in args Object from its current position to
		//		the position defined by (args.left, args.top).
		//
		// args: Object
		//		A hash-map of standard `dojo.Animation` constructor properties
		//		(such as easing: node: duration: and so on). Special args members
		//		are `top` and `left`, which indicate the new position to slide to.
		//
		// example:
		//	|	dojo.fx.slideTo({ node: node, left:"40", top:"50", units:"px" }).play()

		var node = args.node = d.byId(args.node),
			top = null, left = null;

		var init = (function(n){
			return function(){
				var cs = d.getComputedStyle(n);
				var pos = cs.position;
				top = (pos == 'absolute' ? n.offsetTop : parseInt(cs.top) || 0);
				left = (pos == 'absolute' ? n.offsetLeft : parseInt(cs.left) || 0);
				if(pos != 'absolute' && pos != 'relative'){
					var ret = d.position(n, true);
					top = ret.y;
					left = ret.x;
					n.style.position="absolute";
					n.style.top=top+"px";
					n.style.left=left+"px";
				}
			};
		})(node);
		init();

		var anim = d.animateProperty(d.mixin({
			properties: {
				top: args.top || 0,
				left: args.left || 0
			}
		}, args));
		d.connect(anim, "beforeBegin", anim, init);

		return anim; // dojo.Animation
	};

})();

}

if(!dojo._hasResource["dojox.fx.flip"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojox.fx.flip"] = true;
dojo.provide("dojox.fx.flip");










	dojo.experimental("dojox.fx.flip");
	// because ShrinkSafe will eat this up:
	var borderConst = "border",
		widthConst = "Width",
		heightConst = "Height",
		topConst = "Top",
		rightConst = "Right",
		leftConst = "Left",
		bottomConst = "Bottom"
	;

	dojox.fx.flip = function(/*Object*/ args){
		// summary: Animate a node flipping following a specific direction
		//
		// description:
		//		Returns an animation that will flip the
		//		node around a central axis:
		//		if args.dir is "left" or "right" --> y axis
		//		if args.dir is "top" or "bottom" --> x axis
		//
		//		This effect is obtained using a border distorsion applied to a helper node.
		//
		//		The user can specify three background colors for the helper node:
		//		darkColor: the darkest color reached during the animation
		//		lightColor: the brightest color
		//		endColor: the final backgroundColor for the node
        //
        //		depth: Float
		//			 0 <= depth <= 1 overrides the computed "depth"
        //          (0: min distorsion, 1: max distorsion)
        //
        //      whichAnim: String
        //          "first"          : the first half animation
        //          "last"           : the second one
        //          "both" (default) : both
        //
        //      axis: String
        //          "center" (default)    : the node is flipped around his center
        //          "shortside"           : the node is flipped around his "short" (in perspective) side
        //          "longside"            : the node is flipped around his "long" (in perspective) side
        //          "cube"                : the node flips around the central axis of the cube
        //
        //      shift: Integer
        //          node translation, perpendicular to the rotation axis
		//
		//	example:
		//	|	var anim = dojox.fx.flip({
		//	|		node: dojo.byId("nodeId"),
		//	|		dir: "top",
		//	|		darkColor: "#555555",
		//	|		lightColor: "#dddddd",
		//	|		endColor: "#666666",
		//	|		depth: .5,
		//	|		shift: 50,
		//	|		duration:300
		//	|	  });

		var helperNode = dojo.create("div"),
			node = args.node = dojo.byId(args.node),
			s = node.style,
			dims = null,
			hs = null,
			pn = null,
			lightColor = args.lightColor || "#dddddd",
			darkColor = args.darkColor || "#555555",
			bgColor = dojo.style(node, "backgroundColor"),
			endColor = args.endColor || bgColor,
			staticProps = {},
			anims = [],
			duration = args.duration ? args.duration / 2 : 250,
			dir = args.dir || "left",
			pConst = .9,
			transparentColor = "transparent",
			whichAnim = args.whichAnim,
			axis = args.axis || "center",
			depth = args.depth
		;
		// IE6 workaround: IE6 doesn't support transparent borders
		var convertColor = function(color){
			return ((new dojo.Color(color)).toHex() === "#000000") ? "#000001" : color;
		};

		if(dojo.isIE < 7){
			endColor = convertColor(endColor);
			lightColor = convertColor(lightColor);
			darkColor = convertColor(darkColor);
			bgColor = convertColor(bgColor);
			transparentColor = "black";
			helperNode.style.filter = "chroma(color='#000000')";
		}

		var init = (function(n){
			return function(){
				var ret = dojo.coords(n, true);
				dims = {
					top: ret.y,
					left: ret.x,
					width: ret.w,
					height: ret.h
				};
			}
		})(node);
		init();
		// helperNode initialization
		hs = {
			position: "absolute",
			top: dims["top"] + "px",
			left: dims["left"] + "px",
			height: "0",
			width: "0",
			zIndex: args.zIndex || (s.zIndex || 0),
			border: "0 solid " + transparentColor,
			fontSize: "0",
			visibility: "hidden"
		};
		var props = [ {},
			{
				top: dims["top"],
				left: dims["left"]
			}
		];
		var dynProperties = {
			left: [leftConst, rightConst, topConst, bottomConst, widthConst, heightConst, "end" + heightConst + "Min", leftConst, "end" + heightConst + "Max"],
			right: [rightConst, leftConst, topConst, bottomConst, widthConst, heightConst, "end" + heightConst + "Min", leftConst, "end" + heightConst + "Max"],
			top: [topConst, bottomConst, leftConst, rightConst, heightConst, widthConst, "end" + widthConst + "Min", topConst, "end" + widthConst + "Max"],
			bottom: [bottomConst, topConst, leftConst, rightConst, heightConst, widthConst, "end" + widthConst + "Min", topConst, "end" + widthConst + "Max"]
		};
		// property names
		pn = dynProperties[dir];

		// .4 <= pConst <= .9
		if(typeof depth != "undefined"){
			depth = Math.max(0, Math.min(1, depth)) / 2;
			pConst = .4 + (.5 - depth);
		}else{
			pConst = Math.min(.9, Math.max(.4, dims[pn[5].toLowerCase()] / dims[pn[4].toLowerCase()]));
		}
		var p0 = props[0];
		for(var i = 4; i < 6; i++){
			if(axis == "center" || axis == "cube"){ // find a better name for "cube"
				dims["end" + pn[i] + "Min"] = dims[pn[i].toLowerCase()] * pConst;
				dims["end" + pn[i] + "Max"] = dims[pn[i].toLowerCase()] / pConst;
			}else if(axis == "shortside"){
				dims["end" + pn[i] + "Min"] = dims[pn[i].toLowerCase()];
				dims["end" + pn[i] + "Max"] = dims[pn[i].toLowerCase()] / pConst;
			}else if(axis == "longside"){
				dims["end" + pn[i] + "Min"] = dims[pn[i].toLowerCase()] * pConst;
				dims["end" + pn[i] + "Max"] = dims[pn[i].toLowerCase()];
			}
		}
		if(axis == "center"){
			p0[pn[2].toLowerCase()] = dims[pn[2].toLowerCase()] - (dims[pn[8]] - dims[pn[6]]) / 4;
		}else if(axis == "shortside"){
			p0[pn[2].toLowerCase()] = dims[pn[2].toLowerCase()] - (dims[pn[8]] - dims[pn[6]]) / 2;
		}

		staticProps[pn[5].toLowerCase()] = dims[pn[5].toLowerCase()] + "px";
		staticProps[pn[4].toLowerCase()] = "0";
		staticProps[borderConst + pn[1] + widthConst] = dims[pn[4].toLowerCase()] + "px";
		staticProps[borderConst + pn[1] + "Color"] = bgColor;

		p0[borderConst + pn[1] + widthConst] = 0;
		p0[borderConst + pn[1] + "Color"] = darkColor;
		p0[borderConst + pn[2] + widthConst] = p0[borderConst + pn[3] + widthConst] = axis != "cube"
			? (dims["end" + pn[5] +  "Max"] - dims["end" + pn[5] + "Min"]) / 2
			: dims[pn[6]] / 2
		;
		p0[pn[7].toLowerCase()] = dims[pn[7].toLowerCase()] + dims[pn[4].toLowerCase()] / 2 + (args.shift || 0);
		p0[pn[5].toLowerCase()] = dims[pn[6]];

		var p1 = props[1];
		p1[borderConst + pn[0] + "Color"] = { start: lightColor, end: endColor };
		p1[borderConst + pn[0] + widthConst] = dims[pn[4].toLowerCase()];
		p1[borderConst + pn[2] + widthConst] = 0;
		p1[borderConst + pn[3] + widthConst] = 0;
		p1[pn[5].toLowerCase()] = { start: dims[pn[6]], end: dims[pn[5].toLowerCase()] };

		dojo.mixin(hs, staticProps);
		dojo.style(helperNode, hs);
		dojo.body().appendChild(helperNode);

		var finalize = function(){
//			helperNode.parentNode.removeChild(helperNode);
			dojo.destroy(helperNode);
			// fixes a flicker when the animation ends
			s.backgroundColor = endColor;
			s.visibility = "visible";
		};
		if(whichAnim == "last"){
			for(i in p0){
				p0[i] = { start: p0[i] };
			}
			p0[borderConst + pn[1] + "Color"] = { start: darkColor, end: endColor };
			p1 = p0;
		}
		if(!whichAnim || whichAnim == "first"){
			anims.push(dojo.animateProperty({
				node: helperNode,
				duration: duration,
				properties: p0
			}));
		}
		if(!whichAnim || whichAnim == "last"){
			anims.push(dojo.animateProperty({
				node: helperNode,
				duration: duration,
				properties: p1,
				onEnd: finalize
			}));
		}

		// hide the original node
		dojo.connect(anims[0], "play", function(){
			helperNode.style.visibility = "visible";
			s.visibility = "hidden";
		});

		return dojo.fx.chain(anims); // dojo.Animation

	}

	dojox.fx.flipCube = function(/*Object*/ args){
		// summary: An extension to `dojox.fx.flip` providing a more 3d-like rotation
		//
		// description:
		//		An extension to `dojox.fx.flip` providing a more 3d-like rotation.
		//		Behaves the same as `dojox.fx.flip`, using the same attributes and
		//		other standard `dojo.Animation` properties.
		//
		//	example:
		//		See `dojox.fx.flip`
		var anims = [],
			mb = dojo.marginBox(args.node),
			shiftX = mb.w / 2,
			shiftY = mb.h / 2,
			dims = {
				top: {
					pName: "height",
					args:[
						{
							whichAnim: "first",
							dir: "top",
							shift: -shiftY
						},
						{
							whichAnim: "last",
							dir: "bottom",
							shift: shiftY
						}
					]
				},
				right: {
					pName: "width",
					args:[
						{
							whichAnim: "first",
							dir: "right",
							shift: shiftX
						},
						{
							whichAnim: "last",
							dir: "left",
							shift: -shiftX
						}
					]
				},
				bottom: {
					pName: "height",
					args:[
						{
							whichAnim: "first",
							dir: "bottom",
							shift: shiftY
						},
						{
							whichAnim: "last",
							dir: "top",
							shift: -shiftY
						}
					]
				},
				left: {
					pName: "width",
					args:[
						{
							whichAnim: "first",
							dir: "left",
							shift: -shiftX
						},
						{
							whichAnim: "last",
							dir: "right",
							shift: shiftX
						}
					]
				}
			}
		;
		var d = dims[args.dir || "left"],
			p = d.args
		;
		args.duration = args.duration ? args.duration * 2 : 500;
		args.depth = .8;
		args.axis = "cube";
		for(var i = p.length - 1; i >= 0; i--){
			dojo.mixin(args, p[i]);
			anims.push(dojox.fx.flip(args));
		}
		return dojo.fx.combine(anims);
	};
	
	dojox.fx.flipPage = function(/*Object*/ args){
		// summary: An extension to `dojox.fx.flip` providing a page flip like animation.
		//
		// description:
		//		An extension to `dojox.fx.flip` providing a page flip effect.
		//		Behaves the same as `dojox.fx.flip`, using the same attributes and
		//		other standard `dojo.Animation` properties.
		//
		//	example:
		//		See `dojox.fx.flip`
		var n = args.node,
			coords = dojo.coords(n, true),
			x = coords.x,
			y = coords.y,
			w = coords.w,
			h = coords.h,
			bgColor = dojo.style(n, "backgroundColor"),
			lightColor = args.lightColor || "#dddddd",
			darkColor = args.darkColor,
			helperNode = dojo.create("div"),
			anims = [],
			hn = [],
			dir = args.dir || "right",
			pn = {
				left: ["left", "right", "x", "w"],
				top: ["top", "bottom", "y", "h"],
				right: ["left", "left", "x", "w"],
				bottom: ["top", "top", "y", "h"]
			},
			shiftMultiplier = {
				right: [1, -1],
				left: [-1, 1],
				top: [-1, 1],
				bottom: [1, -1]
			}
		;
		dojo.style(helperNode, {
			position: "absolute",
			width  : w + "px",
			height : h + "px",
			top    : y + "px",
			left   : x + "px",
			visibility: "hidden"
		});
		var hs = [];
		for(var i = 0; i < 2; i++){
			var r = i % 2,
				d = r ? pn[dir][1] : dir,
				wa = r ? "last" : "first",
				endColor = r ? bgColor : lightColor,
				startColor = r ? endColor : args.startColor || n.style.backgroundColor
			;
			hn[i] = dojo.clone(helperNode);
			var	finalize = function(x){
					return function(){
						dojo.destroy(hn[x]);
					}
				}(i)
			;
			dojo.body().appendChild(hn[i]);
			hs[i] = {
				backgroundColor: r ? startColor : bgColor
			};
			
			hs[i][pn[dir][0]] = coords[pn[dir][2]] + shiftMultiplier[dir][0] * i * coords[pn[dir][3]] + "px";
			dojo.style(hn[i], hs[i]);
			anims.push(dojox.fx.flip({
			    node: hn[i],
			    dir: d,
			    axis: "shortside",
			    depth: args.depth,
			    duration: args.duration / 2,
			    shift: shiftMultiplier[dir][i] * coords[pn[dir][3]] / 2,
				darkColor: darkColor,
				lightColor: lightColor,
			    whichAnim: wa,
			    endColor: endColor
			}));
			dojo.connect(anims[i], "onEnd", finalize);
		}
		return dojo.fx.chain(anims);
	};
	
	
	dojox.fx.flipGrid = function(/*Object*/ args){
		// summary: An extension to `dojox.fx.flip` providing a decomposition in rows * cols flipping elements
		//
		// description:
		//		An extension to `dojox.fx.flip` providing a page flip effect.
		//		Behaves the same as `dojox.fx.flip`, using the same attributes and
		//		other standard `dojo.Animation` properties and
		//
        //      cols: Integer columns
        //      rows: Integer rows
		//
		//      duration: the single flip duration
		//
		//	example:
		//		See `dojox.fx.flip`
		var rows = args.rows || 4,
			cols = args.cols || 4,
			anims = [],
			helperNode = dojo.create("div"),
			n = args.node,
			coords = dojo.coords(n, true),
			x = coords.x,
			y = coords.y,
			nw = coords.w,
			nh = coords.h,
			w = coords.w / cols,
			h = coords.h / rows,
			cAnims = []
		;
		dojo.style(helperNode, {
			position: "absolute",
			width: w + "px",
			height: h + "px",
			backgroundColor: dojo.style(n, "backgroundColor")
		});
		for(var i = 0; i < rows; i++){
			var r = i % 2,
				d = r ? "right" : "left",
				signum = r ? 1 : -1
			;
			// cloning
			var cn = dojo.clone(n);
			dojo.style(cn, {
				position: "absolute",
				width: nw + "px",
				height: nh + "px",
				top: y + "px",
				left: x + "px",
				clip: "rect(" + i * h + "px," + nw + "px," + nh + "px,0)"
			});
	     	dojo.body().appendChild(cn);
			anims[i] = [];
			for(var j = 0; j < cols; j++){
				var hn = dojo.clone(helperNode),
					l = r ? j : cols - (j + 1)
				;
				var adjustClip = function(xn, yCounter, xCounter){
					return function(){
						if(!(yCounter % 2)){
							dojo.style(xn, {
								clip: "rect(" + yCounter * h + "px," + (nw - (xCounter + 1) * w ) + "px," + ((yCounter + 1) * h) + "px,0px)"
							});
						}else{
							dojo.style(xn, {
								clip: "rect(" + yCounter * h + "px," + nw + "px," + ((yCounter + 1) * h) + "px," + ((xCounter + 1) * w) + "px)"
							});
						}
					}
				}(cn, i, j);
	     		dojo.body().appendChild(hn);
	     		dojo.style(hn, {
	     		    left: x + l * w + "px",
	     		    top: y + i * h + "px",
					visibility: "hidden"
	     		});
				var a = dojox.fx.flipPage({
				   node: hn,
				   dir: d,
				   duration: args.duration || 900,
				   shift: signum * w/2,
				   depth: .2,
				   darkColor: args.darkColor,
				   lightColor: args.lightColor,
				   startColor: args.startColor || args.node.style.backgroundColor
				}),
				removeHelper = function(xn){
					return function(){
						dojo.destroy(xn);
					}
				}(hn)
				;
				dojo.connect(a, "play", this, adjustClip);
				dojo.connect(a, "play", this, removeHelper);
				anims[i].push(a);
			}
			cAnims.push(dojo.fx.chain(anims[i]));
			
		}
		dojo.connect(cAnims[0], "play", function(){
			dojo.style(n, {visibility: "hidden"});
		});
		return dojo.fx.combine(cAnims);
	};

}

if(!dojo._hasResource["dojox.mobile.compat"]){ //_hasResource checks added by build. Do not use _hasResource directly in your code.
dojo._hasResource["dojox.mobile.compat"] = true;
dojo.provide("dojox.mobile.compat");












// summary:
//		CSS3 compatibility module
// description:
//		This module provides support for some of the CSS3 features to dojox.mobile
//		for non-CSS3 browsers, such as IE or Firefox.
//		If you load this module, it directly replaces some of the methods of
//		dojox.mobile instead of subclassing. This way, html pages remains the same
//		regardless of whether this compatibility module is used or not.
//		Recommended usage is as follows. the code below loads dojox.mobile.compat
//		only when isWebKit is true.
//
//		dojo.require("dojox.mobile");
//		
//
//		This module also loads compatibility CSS files, which has -compat.css
//		suffix. You can use either the <link> tag or @import to load theme
//		CSS files. Then, this module searches for the loaded CSS files and loads
//		compatibility CSS files. For example, if you load iphone.css in a page,
//		this module automatically loads iphone-compat.css.
//		If you explicitly load iphone-compat.css with <link> or @import,
//		this module will not load the already loaded file.

if(!dojo.isWebKit){

dojo.extend(dojox.mobile.View, {
	_doTransition: function(fromNode, toNode, transition, dir){
		var anim;
		this.wakeUp(toNode);
		if(!transition || transition == "none"){
			toNode.style.display = "";
			fromNode.style.display = "none";
			toNode.style.left = "0px";
			this.invokeCallback();
		}else if(transition == "slide"){
			var w = fromNode.offsetWidth;
			var s1 = dojo.fx.slideTo({
				node: fromNode,
				duration: 400,
				left: -w*dir,
				top: fromNode.offsetTop
			});
			var s2 = dojo.fx.slideTo({
				node: toNode,
				duration: 400,
				left: 0
			});
			toNode.style.position = "absolute";
			toNode.style.left = w*dir + "px";
			toNode.style.display = "";
			anim = dojo.fx.combine([s1,s2]);
			dojo.connect(anim, "onEnd", this, function(){
				fromNode.style.display = "none";
				toNode.style.position = "relative";
				this.invokeCallback();
			});
			anim.play();
		}else if(transition == "flip"){
			anim = dojox.fx.flip({
				node: fromNode,
				dir: "right",
				depth: 0.5,
				duration: 400
			});
			toNode.style.position = "absolute";
			toNode.style.left = "0px";
			dojo.connect(anim, "onEnd", this, function(){
				fromNode.style.display = "none";
				toNode.style.position = "relative";
				toNode.style.display = "";
				this.invokeCallback();
			});
			anim.play();
		}else if(transition == "fade"){
			anim = dojo.fx.chain([
				dojo.fadeOut({
					node: fromNode,
					duration: 600
				}),
				dojo.fadeIn({
					node: toNode,
					duration: 600
				})
			]);
			toNode.style.position = "absolute";
			toNode.style.left = "0px";
			toNode.style.display = "";
			dojo.style(toNode, "opacity", 0);
			dojo.connect(anim, "onEnd", this, function(){
				fromNode.style.display = "none";
				toNode.style.position = "relative";
				dojo.style(fromNode, "opacity", 1);
				this.invokeCallback();
			});
			anim.play();
		}
	},

	wakeUp: function(node){
		// summary:
		//		Function to force IE to redraw a node since its layout code tends to misrender
		//		in partial draws.
		//	node:
		//		The node to forcibly redraw.
		// tags:
		//		public
		if(dojo.isIE && !node._wokeup){
			node._wokeup = true;
			var disp = node.style.display;
			node.style.display = "";
			var nodes = node.getElementsByTagName("*");
			for(var i = 0, len = nodes.length; i < len; i++){
				var val = nodes[i].style.display;
				nodes[i].style.display = "none";
				nodes[i].style.display = "";
				nodes[i].style.display = val;
			}
			node.style.display = disp;
		}
	}
});

dojo.extend(dojox.mobile.Switch, {
	buildRendering: function(){
		// summary:
		//		Function to simulate the mobile device style switches on
		//		browsers such as IE and FireFox.
		// tags:
		//		protected
		this.domNode = this.srcNodeRef || dojo.doc.createElement("DIV");
		this.domNode.className = "mblSwitch";
		this.domNode.innerHTML =
			  '<div class="mblSwitchInner">'
			+	'<div class="mblSwitchBg mblSwitchBgLeft">'
			+		'<div class="mblSwitchCorner mblSwitchCorner1T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3T"></div>'
			+		'<div class="mblSwitchText mblSwitchTextLeft">'+this.leftLabel+'</div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner1B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3B"></div>'
			+	'</div>'
			+	'<div class="mblSwitchBg mblSwitchBgRight">'
			+		'<div class="mblSwitchCorner mblSwitchCorner1T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3T"></div>'
			+		'<div class="mblSwitchText mblSwitchTextRight">'+this.rightLabel+'</div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner1B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3B"></div>'
			+	'</div>'
			+	'<div class="mblSwitchKnobContainer">'
			+		'<div class="mblSwitchCorner mblSwitchCorner1T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2T"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3T"></div>'
			+		'<div class="mblSwitchKnob"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner1B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner2B"></div>'
			+		'<div class="mblSwitchCorner mblSwitchCorner3B"></div>'
			+	'</div>'
			+ '</div>';
		var n = this.inner = this.domNode.firstChild;
		this.left = n.childNodes[0];
		this.right = n.childNodes[1];
		this.knob = n.childNodes[2];

		dojo.addClass(this.domNode, (this.value == "on") ? "mblSwitchOn" : "mblSwitchOff");
		this[this.value == "off" ? "left" : "right"].style.display = "none";
	},

	_changeState: function(/*String*/state){
		// summary:
		//		Function to toggle the switch state on the switch
		// state:
		//		Thhe state to toggle, switch 'on' or 'off'
		// tags:
		//		private
		if(!this.inner.parentNode || !this.inner.parentNode.tagName){
			dojo.addClass(this.domNode, (state == "on") ? "mblSwitchOn" : "mblSwitchOff");
			return;
		}
		var pos;
		if(this.inner.offsetLeft == 0){ // currently ON
			if(state == "on"){ return; }
			pos = -53;
		}else{ // currently OFF
			if(state == "off"){ return; }
			pos = 0;
		}

		var a = dojo.fx.slideTo({
			node: this.inner,
			duration: 500,
			left: pos
		});
		var _this = this;
		dojo.connect(a, "onEnd", function(){
			_this[state == "off" ? "left" : "right"].style.display = "none";
		});
		a.play();
	}
});

if(dojo.isIE || dojo.isBB){

dojo.extend(dojox.mobile.RoundRect, {
	buildRendering: function(){
		// summary:
		//		Function to simulate the borderRadius appearance on IE, since
		//		IE does not support this CSS style.
		// tags:
		//		protected
		dojox.mobile.createRoundRect(this);
		this.domNode.className = "mblRoundRect";
	}
});

dojox.mobile.RoundRectList._addChild = dojox.mobile.RoundRectList.prototype.addChild;
dojo.extend(dojox.mobile.RoundRectList, {
	buildRendering: function(){
		// summary:
		//		Function to simulate the borderRadius appearance on IE, since
		//		IE does not support this CSS style.
		// tags:
		//		protected
		dojox.mobile.createRoundRect(this, true);
		this.domNode.className = "mblRoundRectList";
	},

	postCreate: function(){
		this.redrawBorders();
	},

	addChild: function(widget){
		dojox.mobile.RoundRectList._addChild.apply(this, arguments);
		this.redrawBorders();
		if(dojox.mobile.applyPngFilter){
			dojox.mobile.applyPngFilter(widget.domNode);
		}
	},

	redrawBorders: function(){
		// summary:
		//		Function to adjust the creation of RoundRectLists on IE.
		//		Removed undesired styles.
		// tags:
		//		public

		// Remove a border of the last ListItem.
		// This is for browsers that do not support the last-child CSS pseudo-class.

		var lastChildFound = false;
		for(var i = this.containerNode.childNodes.length - 1; i >= 0; i--){
			var c = this.containerNode.childNodes[i];
			if(c.tagName == "LI"){
				c.style.borderBottomStyle = lastChildFound ? "solid" : "none";
				lastChildFound = true;
			}
		}
	}
});

dojo.extend(dojox.mobile.EdgeToEdgeList, {
	buildRendering: function(){
		this.domNode = this.containerNode = this.srcNodeRef || dojo.doc.createElement("UL");
		this.domNode.className = "mblEdgeToEdgeList";
	}
});

if(dojox.mobile.IconContainer){

dojox.mobile.IconContainer._addChild = dojox.mobile.IconContainer.prototype.addChild;
dojo.extend(dojox.mobile.IconContainer, {
	addChild: function(widget){
		dojox.mobile.IconContainer._addChild.apply(this, arguments);
		if(dojox.mobile.applyPngFilter){
			dojox.mobile.applyPngFilter(widget.domNode);
		}
	}
});

} // if(dojox.mobile.IconContainer)

dojo.mixin(dojox.mobile, {
	createRoundRect: function(_this, isList){
		// summary:
		//		Function to adjust the creation of rounded rectangles on IE.
		//		Deals with IE's lack of borderRadius support
		// tags:
		//		public
		var i;
		_this.domNode = dojo.doc.createElement("DIV");
		_this.domNode.style.padding = "0px";
		_this.domNode.style.backgroundColor = "transparent";
		_this.domNode.style.borderStyle = "none";
		_this.containerNode = dojo.doc.createElement(isList?"UL":"DIV");
		_this.containerNode.className = "mblRoundRectContainer";
		if(_this.srcNodeRef){
			_this.srcNodeRef.parentNode.replaceChild(_this.domNode, _this.srcNodeRef);
			for(i = 0, len = _this.srcNodeRef.childNodes.length; i < len; i++){
				_this.containerNode.appendChild(_this.srcNodeRef.removeChild(_this.srcNodeRef.firstChild));
			}
			_this.srcNodeRef = null;
		}
		_this.domNode.appendChild(_this.containerNode);

		for(i = 0; i <= 5; i++){
			var top = dojo.create("DIV");
			top.className = "mblRoundCorner mblRoundCorner"+i+"T";
			_this.domNode.insertBefore(top, _this.containerNode);

			var bottom = dojo.create("DIV");
			bottom.className = "mblRoundCorner mblRoundCorner"+i+"B";
			_this.domNode.appendChild(bottom);
		}
	}
});

if(dojox.mobile.ScrollableView){

dojo.extend(dojox.mobile.ScrollableView, {
	postCreate: function(){
		// On IE, margin-top of the first child does not seem to be effective,
		// probably because padding-top is specified for containerNode
		// to make room for a fixed header. This dummy node is a workaround for that.
		var dummy = dojo.create("DIV", {className:"mblDummyForIE", innerHTML:"&nbsp;"}, this.containerNode, "first");
		dojo.style(dummy, {
			position: "relative",
			marginBottom: "-2px",
			fontSize: "1px"
		});
	}
});

} // if(dojox.mobile.ScrollableView)

} // if(dojo.isIE)

if(dojo.isIE <= 6){
	dojox.mobile.applyPngFilter = function(root){
		root = root || dojo.body();
		var nodes = root.getElementsByTagName("IMG");
		var blank = dojo.moduleUrl("dojo", "resources/blank.gif");
		for(var i = 0, len = nodes.length; i < len; i++){
			var img = nodes[i];
			var w = img.offsetWidth;
			var h = img.offsetHeight;
			if(w === 0 || h === 0){
				// The reason why the image has no width/height may be because
				// display is "none". If that is the case, let's change the
				// display to "" temporarily and see if the image returns them.
				if(dojo.style(img, "display") != "none"){ continue; }
				img.style.display = "";
				w = img.offsetWidth;
				h = img.offsetHeight;
				img.style.display = "none";
				if(w === 0 || h === 0){ continue; }
			}
			var src = img.src;
			if(src.indexOf("resources/blank.gif") != -1){ continue; }
			img.src = blank;
			img.runtimeStyle.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(src='" + src+"')";
			img.style.width = w + "px";
			img.style.height = h + "px";
		}
	};
} // if(dojo.isIE <= 6)

dojox.mobile.loadCss = function(/*String|Array*/files){
	// summary:
	//		Function to load and register CSS files with the page
	//	files: String|Array
	//		The CSS files to load and register with the page.
	// tags:
	//		private
	if(!dojo.global._loadedCss){
		var obj = {};
		dojo.forEach(dojox.mobile.getCssPaths(), function(path){
			obj[path] = true;
		});
		dojo.global._loadedCss = obj;
	}
	if(!dojo.isArray(files)){ files = [files]; }
	for(var i = 0; i < files.length; i++){
		var file = files[i];
		if(!dojo.global._loadedCss[file]){
			dojo.global._loadedCss[file] = true;
			if(dojo.doc.createStyleSheet){
				// for some reason, IE hangs when you try to load
				// multiple css files almost at once.
				setTimeout(function(file){
					return function(){
						dojo.doc.createStyleSheet(file);
					};
				}(file), 0);
			}else{
				var link = dojo.doc.createElement("link");
				link.href = file;
				link.type = "text/css";
				link.rel = "stylesheet";
				var head = dojo.doc.getElementsByTagName('head')[0];
				head.appendChild(link);
			}
		}
	}
};

dojox.mobile.getCssPaths = function(){
	var paths = [];
	var i, j;

	// find @import
	var s = dojo.doc.styleSheets;
	for(i = 0; i < s.length; i++){
		var r = s[i].cssRules || s[i].imports;
		if(!r){ continue; }
		for(j = 0; j < r.length; j++){
			if(r[j].href){
				paths.push(r[j].href);
			}
		}
	}
	
	// find <link>
	var elems = dojo.doc.getElementsByTagName("link");
	for(i = 0, len = elems.length; i < len; i++){
		if(elems[i].href){
			paths.push(elems[i].href);
		}
	}
	return paths;
};

dojox.mobile.loadCompatPattern = /\/themes\/(domButtons|buttons|iphone|android).*\.css$/;

dojox.mobile.loadCompatCssFiles = function(){
	// summary:
	//		Function to perform page-level adjustments on browsers such as
	//		IE and firefox.  It loads compat specific css files into the
	//		page header.
	var paths = dojox.mobile.getCssPaths();
	for(var i = 0; i < paths.length; i++){
		var href = paths[i];
		if(href.match(dojox.mobile.loadCompatPattern) && href.indexOf("-compat.css") == -1){
			var compatCss = href.substring(0, href.length-4)+"-compat.css";
			dojox.mobile.loadCss(compatCss);
		}
	}
};

dojox.mobile.hideAddressBar = function(){
	// nop
};

dojo.addOnLoad(function(){
	if(dojo.config["mblLoadCompatCssFiles"] !== false){
		dojox.mobile.loadCompatCssFiles();
	}
	if(dojox.mobile.applyPngFilter){
		dojox.mobile.applyPngFilter();
	}
});

} // end of if(!dojo.isWebKit){

}

