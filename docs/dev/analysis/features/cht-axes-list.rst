
Multiple Chart Value or Category Axes
=====================================

PowerPoint chart axes come in four varieties: category axis, value axis, date
axis, and series axis. A series axis only appears on a 3D chart and is also
known as its depth axis.

A chart may have two category axes and/or up to four value axes. In the
simplest cases, there are zero or one of each type and you access them
with ``chart.value_axis`` and ``chart.category_axis``.

A category axis may appear as either the horizontal or vertical axis,
depending upon the chart type. Likewise for a value axis.


PowerPoint behavior
-------------------

Proposed python-pptx protocol for lists of axes::

    >>> # One value_axes in our chart
    >>> chart.value_axis
    <pptx.chart.axis.ValueAxis object at 0x7f7bc240f750>
    >>> chart.value_axes_list
    [<pptx.chart.axis.ValueAxis object at 0x7f7bc240f750>]
    >>>
    >>> # Zero value_axes
    >>> chart.value_axis
    ...
    ValueError: chart has no value axis
    >>> chart.value_axis
    []

Proposed python-pptx protocol for working with axes::
    >>> chart.value_axis.axisId # ro
    '123456789'
    >>> chart.value_axis.crossAx # rw
    '6789101112'
    >>> chart.value_axis.crosses # rw
    'autoZero' # or 'max' or numeric string
    >>> chart.value_axis.position # rw
    'b' # or 'l' or 'r'
    >>> chart.value_axis.format # rw
    'General' # or any number format string

Open questions
--------------

* How much validation should be done when writing axes values?
  - crossAx could be set to cross a nonexistant axis
  - changing the position from bottom to a side or *vice versa* could be bad
  - allow nonsense values for crosses and format?
* ChartData API for creating data with secondary axes
  - could make ``add_secondary_series`` method
  - could add argument e.g. ``chart_data.add_series(name, d, axis='secondary')``
* Should some properties of axes be controlled through ChartData?
  - @huandzh implemented control of numeric format through ``add_series``

XML specimens
-------------

.. highlight:: xml

Example XML for a chart with two series, one of which uses a secondary axis::

  <c:chart>
    <c:plotArea>
      <c:layout/>
      <c:scatterChart>
        <c:scatterStyle val="lineMarker"/>
        <c:ser>
          <c:idx val="0"/>
          <c:order val="0"/>
          <c:tx>
            <c:strRef>
              <c:f>Sheet1!$B$1</c:f>
              <c:strCache>
                <c:ptCount val="1"/>
                <c:pt idx="0">
                  <c:v>Left Values</c:v>
                </c:pt>
              </c:strCache>
            </c:strRef>
          </c:tx>
          <c:spPr>
            <a:ln w="28575">
              <a:noFill/>
            </a:ln>
          </c:spPr>
          <c:xVal>
            <c:numRef>
              <c:f>Sheet1!$A$2:$A$4</c:f>
              <c:numCache>
                <c:formatCode>General</c:formatCode>
                <c:ptCount val="3"/>
                <c:pt idx="0">
                  <c:v>0.7</c:v>
                </c:pt>
                <c:pt idx="1">
                  <c:v>1.8</c:v>
                </c:pt>
                <c:pt idx="2">
                  <c:v>2.6</c:v>
                </c:pt>
              </c:numCache>
            </c:numRef>
          </c:xVal>
          <c:yVal>
            <c:numRef>
              <c:f>Sheet1!$B$2:$B$4</c:f>
              <c:numCache>
                <c:formatCode>General</c:formatCode>
                <c:ptCount val="3"/>
                <c:pt idx="0">
                  <c:v>2.7</c:v>
                </c:pt>
                <c:pt idx="1">
                  <c:v>3.2</c:v>
                </c:pt>
                <c:pt idx="2">
                  <c:v>0.8</c:v>
                </c:pt>
              </c:numCache>
            </c:numRef>
          </c:yVal>
        </c:ser>
        <c:axId val="68494848"/>
        <c:axId val="68496384"/>
      </c:scatterChart>
      <c:scatterChart>
        <c:scatterStyle val="lineMarker"/>
        <c:ser>
          <c:idx val="1"/>
          <c:order val="1"/>
          <c:tx>
            <c:strRef>
              <c:f>Sheet1!$C$1</c:f>
              <c:strCache>
                <c:ptCount val="1"/>
                <c:pt idx="0">
                  <c:v>Right Values</c:v>
                </c:pt>
              </c:strCache>
            </c:strRef>
          </c:tx>
          <c:spPr>
            <a:ln w="28575">
              <a:noFill/>
            </a:ln>
          </c:spPr>
          <c:xVal>
            <c:numRef>
              <c:f>Sheet1!$A$2:$A$4</c:f>
              <c:numCache>
                <c:formatCode>General</c:formatCode>
                <c:ptCount val="3"/>
                <c:pt idx="0">
                  <c:v>0.7</c:v>
                </c:pt>
                <c:pt idx="1">
                  <c:v>1.8</c:v>
                </c:pt>
                <c:pt idx="2">
                  <c:v>2.6</c:v>
                </c:pt>
              </c:numCache>
            </c:numRef>
          </c:xVal>
          <c:yVal>
            <c:numRef>
              <c:f>Sheet1!$C$2:$C$4</c:f>
              <c:numCache>
                <c:formatCode>General</c:formatCode>
                <c:ptCount val="3"/>
                <c:pt idx="0">
                  <c:v>-4</c:v>
                </c:pt>
                <c:pt idx="1">
                  <c:v>-5</c:v>
                </c:pt>
                <c:pt idx="2">
                  <c:v>-2</c:v>
                </c:pt>
              </c:numCache>
            </c:numRef>
          </c:yVal>
        </c:ser>
        <c:axId val="68512000"/>
        <c:axId val="68510464"/>
      </c:scatterChart>
      <c:valAx>
        <c:axId val="68494848"/>
        <c:scaling>
          <c:orientation val="minMax"/>
        </c:scaling>
        <c:axPos val="b"/>
        <c:title>
          <c:tx>
            <c:rich>
              <a:bodyPr/>
              <a:lstStyle/>
              <a:p>
                <a:pPr>
                  <a:defRPr/>
                </a:pPr>
                <a:r>
                  <a:rPr lang="en-US" dirty="0" err="1" smtClean="0"/>
                  <a:t>primary_horz_axis</a:t>
                </a:r>
                <a:endParaRPr lang="en-US" dirty="0"/>
              </a:p>
            </c:rich>
          </c:tx>
          <c:layout/>
        </c:title>
        <c:numFmt formatCode="General" sourceLinked="1"/>
        <c:tickLblPos val="nextTo"/>
        <c:crossAx val="68496384"/>
        <c:crosses val="autoZero"/>
        <c:crossBetween val="midCat"/>
      </c:valAx>
      <c:valAx>
        <c:axId val="68496384"/>
        <c:scaling>
          <c:orientation val="minMax"/>
        </c:scaling>
        <c:axPos val="l"/>
        <c:majorGridlines/>
        <c:title>
          <c:tx>
            <c:rich>
              <a:bodyPr rot="-5400000" vert="horz"/>
              <a:lstStyle/>
              <a:p>
                <a:pPr>
                  <a:defRPr/>
                </a:pPr>
                <a:r>
                  <a:rPr lang="en-US" dirty="0" err="1" smtClean="0"/>
                  <a:t>primary_vert_axis</a:t>
                </a:r>
                <a:endParaRPr lang="en-US" dirty="0"/>
              </a:p>
            </c:rich>
          </c:tx>
          <c:layout/>
        </c:title>
        <c:numFmt formatCode="General" sourceLinked="1"/>
        <c:tickLblPos val="nextTo"/>
        <c:crossAx val="68494848"/>
        <c:crosses val="autoZero"/>
        <c:crossBetween val="midCat"/>
      </c:valAx>
      <c:valAx>
        <c:axId val="68510464"/>
        <c:scaling>
          <c:orientation val="minMax"/>
        </c:scaling>
        <c:axPos val="r"/>
        <c:title>
          <c:tx>
            <c:rich>
              <a:bodyPr rot="-5400000" vert="horz"/>
              <a:lstStyle/>
              <a:p>
                <a:pPr>
                  <a:defRPr/>
                </a:pPr>
                <a:r>
                  <a:rPr lang="en-US" dirty="0" err="1" smtClean="0"/>
                  <a:t>Secondary_vert_axis</a:t>
                </a:r>
                <a:endParaRPr lang="en-US" dirty="0"/>
              </a:p>
            </c:rich>
          </c:tx>
          <c:layout/>
        </c:title>
        <c:numFmt formatCode="General" sourceLinked="1"/>
        <c:tickLblPos val="nextTo"/>
        <c:crossAx val="68512000"/>
        <c:crosses val="max"/>
        <c:crossBetween val="midCat"/>
      </c:valAx>
      <c:valAx>
        <c:axId val="68512000"/>
        <c:scaling>
          <c:orientation val="minMax"/>
        </c:scaling>
        <c:delete val="1"/>
        <c:axPos val="b"/>
        <c:title>
          <c:tx>
            <c:rich>
              <a:bodyPr/>
              <a:lstStyle/>
              <a:p>
                <a:pPr>
                  <a:defRPr/>
                </a:pPr>
                <a:r>
                  <a:rPr lang="en-US" dirty="0" err="1" smtClean="0"/>
                  <a:t>secondary_horz_axis</a:t>
                </a:r>
                <a:endParaRPr lang="en-US" dirty="0"/>
              </a:p>
            </c:rich>
          </c:tx>
          <c:layout/>
        </c:title>
        <c:numFmt formatCode="General" sourceLinked="1"/>
        <c:tickLblPos val="none"/>
        <c:crossAx val="68510464"/>
        <c:crosses val="autoZero"/>
        <c:crossBetween val="midCat"/>
      </c:valAx>
    </c:plotArea>
    <c:legend>
      <c:legendPos val="t"/>
      <c:layout/>
    </c:legend>
    <c:plotVisOnly val="1"/>
  </c:chart>

The chart can be seen at https://cloud.githubusercontent.com/assets/8269566/5598807/60fa7770-928a-11e4-9ffb-671b3effbd5e.png
