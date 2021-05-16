o associative






## API
```haskell
o :: Chart -> Chart

-- Need atleast two points for line chart
-- Line Chart
line :: [(number, number)] -> Line
interpolate :: Line -> Line
lineWidth :: Int -> Line -> Line
lineDash :: Line -> Line

-- Scatter Chart
scatter :: [(number, number)] -> Scatter
markerSize :: Int -> ScatterChart -> Scatter
jitter :: Int -> ScatterChart -> Scatter

-- Bar Chart
bar :: [(string, number)] -> BarChart
barWidth :: Int -> BarChart -> BarChart
barSpacing :: Int -> BarChart -> BarChart


-- Distributive and idempotent functions
-- These ones are anihilated by overlay

xTicks :: [Number] -> Chart -> Chart
yTicks :: [Number] -> Chart -> Chart
xLabel :: String -> Chart -> Chart
yLabel :: String -> Chart -> Chart
title :: String -> Chart -> Chart
legend :: Chart -> Chart
color :: Colour -> Chart -> Chart


-- Rendering
display :: Chart -> Html msg
```


## Laws
`o` and `empty` form a monoid
```
forall (c :: Chart) . c `o` empty = empty `o` c = c 
forall (c1 :: Chart) (c2 :: Chart) (c3 :: Chart). c1 `o` (c2 `o` c3) = (c1 `o` c2) `o` c3
```

<!-- Idempotent decoration which are distributive with each other but not themselves.  -->

<!-- Overlayng will anihilate these operations -->
`xTicks ts` is an idempotent function
```
forall (c :: Chart) (a1 :: [Number]) (a2 :: [Number]) . xTicks a1 $ xTicks a2 c = xTicks a1 c
```

`yTicks ts` is an idempotent function 
```
forall (c :: Chart) (a1 :: [Number]) (a2 :: [Number]) . yTicks a1 $ yTicks a2 c = yTicks a1 c
```

`xLabel s` is an idempotent function 
```
forall (c :: Chart) (s1 :: String) (s2 :: String) . xLabel s1 $ xLabel s2 c = xLabel s1 c
```

`yLabel s` is an idempotent function 
```
forall (c :: Chart) (s1 :: String) (s2 :: String) . yLabel s1 $ yLabel s2 = yLabel s1 c
```

`xTicks xts` and `yTicks yts` are distributive
forall (c :: Chart) (xts :: [Number]) (yts :: [Number]) . xTicks xts $ yTicks yts c = yTicks yts $ xTicks xts c 


`xTicks xts` and `xLabel s` are distributive
forall (c :: Chart) (xts :: [Number]) (yts :: [Number]) . xTicks xts $ yTicks yts c = yTicks yts $ xTicks xts c


<!-- Default settings when certain decorations are not used-->

- Gridding
- Should this be broken up into several types?
- Alternative Representation is to have a labelled graph type, maybe visualise as a   category


Also like colour

<!-- Scatter plot specific stuff -->
- Marker size
- Marker Shape
- Jittering

<!-- Line plot specific stuff -->
- Line smoothing
- Line size
- Dashed lines

<!-- Graph labelling -->
- xTicks
- yTicks
- yLabel
- xLabel
- Title

<!-- Gridding -->

<!-- Other Plots -->
- Area plots
- Legends
- Bar charts
- Box Plots
- Histograms

<!-- Longterm goals -->
- Gridding
- Interactivity
- Manipulation
- Animation