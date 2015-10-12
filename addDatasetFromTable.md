New function added to Layout.js so you can get labels from a table

```

PlotKit.Layout.prototype.addDatasetFromTableWithLabels = function(name, tableElement, xcol, ycol, lcol) {
	var isNil = MochiKit.Base.isUndefinedOrNull;
	var scrapeText = MochiKit.DOM.scrapeText;
	var strip = MochiKit.Format.strip;
	
	if (isNil(xcol))
		xcol = 0;
	if (isNil(ycol))
		ycol = 1;

    var rows = tableElement.tBodies[0].rows;
    var data = new Array();
    var labs = new Array();
    
    if (!isNil(rows)) {
        for (var i = 0; i < rows.length; i++) {
            data.push([parseFloat(strip(scrapeText(rows[i].cells[xcol]))),
                       parseFloat(strip(scrapeText(rows[i].cells[ycol])))]);
                       
            labs.push( {v: parseFloat(strip(scrapeText(rows[i].cells[xcol]))),
                       label: strip(scrapeText(rows[i].cells[lcol]))});
        }
        this.addDataset(name, data);
        this.options.xTicks = labs;
        return true;
    }
    return false;
};

```