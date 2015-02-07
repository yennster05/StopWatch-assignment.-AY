# StopWatch-assignment.-AY
var win = Ti.UI.createWindow({

backgroundColor: '#ffffff',

layout: 'vertical'

});

var timeView = Ti.UI.createView({

top:0,

width: '100%',

height: '30%',

backgroundColor: '#1C1C1C'

});

var timerlabel = Ti.UI.createLabel ({

color: '#404040',

text: 'READY?',

height: Ti.UI.SIZE,

textAlign: 'center',

veticalAlign: Ti.UI.TEXT_VERTICAL_ALIGNMENT_CENTER,

font:{

fontSize: '55sp',

fontWeight: 'bold',

}

});

timeView.add(timerlabel);

win.add(timeView);

win.open();

var minlabel = Titanium.UI.createLabel({

text: 'Mins',

top: 55,

left: 125,

});

var seclabel = Titanium.UI.createLabel({

text: 'Secs',

top: 55,

right: 105,

});

var buttonsView = Ti.UI.createView({

width: '100%',

height: '10%',

layout: 'horizontal'

});

var ButtonStartLap = Ti.UI.createButton({

title: 'GO!',

color: '#C0BFBF',

width: '50%',

height: Ti.UI.FILL,

backgroundColor: '#727F7F',

font: {

fontSize: '25sp',

fontWeight: 'bold'

}

});

var button02 = Titanium.UI.createButton({

title:'RESET',

top: 90,

right: 10,

width: 100,

height: 50

});

var ButtonStopReset = Ti.UI.createButton({

title: 'STOP',

color: '#C0BFBF',

width: '50%',

height: Ti.UI.FILL,

backgroundColor: '#404040',

font: {

fontSize: '25sp',

fontWeight: 'bold',

}

});

var _startStopwatch = function() {

timerlabel.value = '00:00:00.0';

var startTime = new Date();

var _updateTimer = function updateTimer() {

var UNIT_HOUR = 60 * 60 * 1000;

var UNIT_MINUTE = 60 * 1000;

var UNIT_SEC = 1000;

var now = new Date();

var diff = now.getTime() - startTime.getTime();

var hour = Math.floor(diff / UNIT_HOUR);

var minute = Math.floor((diff - hour * UNIT_HOUR) / UNIT_MINUTE);

var sec = Math.floor((diff - hour * UNIT_HOUR - minute * UNIT_MINUTE) / UNIT_SEC);

var msec = Math.floor(diff % UNIT_SEC);

timerlabel.text = ('0' + hour).slice(-2) + ':' + ('0' + minute).slice(-2) + ':' + ('0' + sec).slice(-2) + '.' + ('00' + msec).slice(-1);

};

intervalid = setInterval(_updateTimer, 3);

button02.title = 'STOP';

};

var _stopStopwatch = function() {

clearInterval(intervalid);

};

var started = false;

var intervalid = null;

buttonsView.add(ButtonStopReset);

buttonsView.add(ButtonStartLap);

win.add(buttonsView);

ButtonStartLap.addEventListener('click',function(e) {

if (!started) {

_startStopwatch();

started = true;

}

});

ButtonStopReset.addEventListener('click',function(e) {

if (started) {

_stopStopwatch();

started = false;

}

timerlabel.text = '00:00:00.0';
});
