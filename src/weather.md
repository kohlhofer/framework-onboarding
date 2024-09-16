# Weather report

```js
const forecast = FileAttachment("./data/forecast.json").json();

function temperaturePlot(data, {width} = {}) {
  return Plot.plot({
    title: "Hourly temperature forecast",
    width,
    x: {type: "utc", ticks: "day", label: null},
    y: {grid: true, inset: 10, label: "Degrees (F)"},
    marks: [
      Plot.lineY(data.properties.periods, {
        x: "startTime",
        y: "temperature",
        z: null, // varying color, not series
        stroke: "temperature",
        curve: "step-after"
      })
    ]
  });
}

function showMap(data) {

    const div = display(document.createElement("div"));
    div.style = "height: 400px;";

    const map = L.map(div)
        .setView([data.geometry.coordinates[0][1][1],data.geometry.coordinates[0][1][0]], 12);

    L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
})
.addTo(map);

L.geoJSON(data.geometry).addTo(map);

return div;
}
```

```js
display(temperaturePlot(forecast));
display(showMap(forecast));
```

