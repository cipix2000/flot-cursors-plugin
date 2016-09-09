[![Stories in Ready](https://badge.waffle.io/cipix2000/flot-cursors-plugin.png?label=ready&title=Ready)](https://waffle.io/cipix2000/flot-cursors-plugin) [![Build Status](https://travis-ci.org/cipix2000/flot-cursors-plugin.svg?branch=master)](https://travis-ci.org/cipix2000/flot-cursors-plugin)

flot.cursors
============

This is a plugin for jQuery flot to create cursors. Cursors are used to measure various values on the graph. You can have multiple cursors on a graph

This plugin is based on another plugin `jQuery.flot.crosshair.js` which can be found in the flot chart package at <http://www.flotcharts.org/>

Options
-------

The plugin supports these options:

```javascript
    cursors: [
        {
            name: 'string'
            mode: null or 'x' or 'y' or 'xy',
            color: color,
            lineWidth: number,
            position: {
                relativeX or x or x2 or x3 ..: number,
                relativeY or y or y2 or y3 ..: number,
            },
            showLabel: true or false,
            snapToPlot: number,
            symbol: 'cross', 'triangle' ...,
            movable: true or false,
            mouseButton: 'all' or 'left' or 'right' or 'middle',
            dashes: number,
            showIntersections: true or false or array,
            intersectionColor: color,
            intersectionLabelPosition: 'bottom-right' or 'bottom-left' or 'top-right' or 'top-left',
            fontSize: number
        },
        <more cursors if needed>
    ]
```

**name** is a string containing the name of the cursor.

**mode** is one of "x", "y" or "xy". The "x" mode enables a vertical cursor that lets you trace the values on the x axis, "y" enables a horizontal cursor and "xy" enables them both. "xy" is default.

**color** is the color of the cursor (default is "rgba(170, 0, 0, 0.80)")

**lineWidth** is the width of the drawn lines (default is 1). Setting lineWidth to zero creates an invisible cursor.

**position** position of the cursor. It can be specified relative to the canvas, using a *relativeX, relativeY* pair of coordinates which are expressed as a number between 0 and 1. It can be also specified using axis based coordinates ( *x, x2, x3 .., y, y2, y3* ).

**showLabel** if true the name of the cursor will be displayed next to the cursor manipulator.

**showValuesRelativeToSeries** if present and is numeric the coordinate of cursor (relative to the specified series of data) will be displayed next to the cursor manipulator.

**snapToPlot** specifies a plot to which the cursor will snap. If not specified (or undefined) the cursor will be free.

**symbol** a shape ('cross', 'triangle' ...). The cursor manipulator will have this shape. Set to 'none' to draw no symbol.

**movable** if true, the cursor can be moved with the mouse. Default is true.

**mouseButton** is which mouse button is used to move the cursor. Note that this may not be compatible with IE 8. Default is 'all'.

**dashes** the number of dashes you want in the line. Set to 1 to get a solid line without dashes. Default is 1.

**showIntersections** if true the intersection with the plots will be displayed as grey rectangles. Can be set to an array of series indices to only show intersections with those series. Default is false.

**intersectionColor** sets the color of the boxes drawn at intersections, and also the color of the text showing the value at the intersection. Default is 'darkgray'.

**intersectionLabelPosition** sets where the intersection label text appears, relative to the intersection. Default is 'bottom-right'.

**fontSize** sets the font size of the cursor labels and intersection value labels. Default is 10.


Public Methods and events
-------------------------


The plugin adds some public methods to the chart:

* getCursors()

    Returns a list containing all the cursors

* addCursor(options)

    creates a new cursor with the parameters specified in options.

* removeCursor(cursorToRemove)

    remove the specified cursor from the plot. cursorToRemove is a cursor
    reference to one of the cursors obtained with getCursors()

* setCursor ( cursor , options)

    changes one or more cursor properties.

Everytime one or more cursors changes state a *cursorupdates* event is emitted on the chart container.
These events are emitted in one of these situations:

* cursor added
* cursor removed
* cursor moved
* intersections of the cursors with the plots changed due to chart data changes


How to use
----------

```javascript
var myFlot = $.plot( $("#graph"), ...,
{
    ...
    cursors: [
        { name: 'Green cursor', mode: 'xy', color: 'green' },
        { name: 'Red cursor', mode: 'xy', color: 'red' }
    ]
    ...
});

$("#graph").bind("cursorupdates", function (event, cursordata) {
    cursordata.forEach(function (cursor) {
        console.log("Cursor " + cursor.cursor + " intersections:");
        cursor.points.forEach(function (point) {
            console.log("x:" + point.x + " y: " + point.y);
        });
    });
});
```    

Examples and tests
------------------

jquery.flot.cursors is available under the MIT license.

Interactive example: <https://rawgit.com/cipix2000/flot-cursors-plugin/master/example.html>

Related plugins
---------------

flot-cursors-legend-plugin at <https://github.com/cipix2000/flot-cursors-legend-plugin> provides a legend for cursors
