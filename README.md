TimeSeries.jl
============
[![Build Status](https://travis-ci.org/JuliaStats/TimeSeries.jl.png)](https://travis-ci.org/JuliaStats/TimeSeries.jl)

#### Installation

````julia
julia> Pkg.add("TimeSeries")
````
Additionally, the unregistered MarketData package includes some `const` objects that include TimeArray objects. These
objects are historical price time series and are used in testing and benchmarking mostly. You may find it useful to 
clone the package and take TimeSeries functionality through some paces with these objects. 

````julia
julia> Pkg.clone("git://github.com/JuliaQuant/MarketData.jl.git")
````

Alternately, you can create some dummy data with this code block.

````julia
d = [date(1980,1,1):date(2015,1,1)];
t = TimeArray(d,rand(length(d)),["test"])
````

#### Quick tour of current API

````julia
julia> using TimeSeries, MarketData

julia> ohlc
505x6 TimeArray{Float64,2} 1980-01-03 to 1981-12-31

             Open    High    Low     Close   Volume       Adj Cl
1980-01-03 | 105.76  106.08  103.26  105.22  50480000.00  105.22
1980-01-04 | 105.22  107.08  105.09  106.52  39130000.00  106.52
1980-01-07 | 106.52  107.80  105.80  106.81  44500000.00  106.81
1980-01-08 | 106.81  109.29  106.29  108.95  53390000.00  108.95
...
1981-12-24 | 122.31  123.06  121.57  122.54  23940000.00  122.54
1981-12-28 | 122.54  123.36  121.73  122.27  28320000.00  122.27
1981-12-29 | 122.27  122.90  121.12  121.67  35300000.00  121.67
1981-12-30 | 121.67  123.11  121.04  122.30  42960000.00  122.30
1981-12-31 | 122.30  123.42  121.57  122.55  40780000.00  122.55

julia> ohlc[1]
1x6 TimeArray{Float64,2} 1980-01-03 to 1980-01-03

             Open    High    Low     Close   Volume       Adj Cl
1980-01-03 | 105.76  106.08  103.26  105.22  50480000.00  105.22


julia> ohlc[1:2]
2x6 TimeArray{Float64,2} 1980-01-03 to 1980-01-04

             Open    High    Low     Close   Volume       Adj Cl
1980-01-03 | 105.76  106.08  103.26  105.22  50480000.00  105.22
1980-01-04 | 105.22  107.08  105.09  106.52  39130000.00  106.52

julia> ohlc[[firstday, tenthday]]
2x6 TimeArray{Float64,2} 1980-01-03 to 1980-01-16

             Open    High    Low     Close   Volume       Adj Cl
1980-01-03 | 105.76  106.08  103.26  105.22  50480000.00  105.22
1980-01-16 | 111.14  112.90  110.38  111.05  67700000.00  111.05


julia> ohlc["Low"][1:2]
2x1 TimeArray{Float64,2} 1980-01-03 to 1980-01-04

             Low
1980-01-03 | 103.26
1980-01-04 | 105.09

julia> ohlc["Open", "Close"][1:2]
2x2 TimeArray{Float64,2} 1980-01-03 to 1980-01-04

             Open    Close
1980-01-03 | 105.76  105.22
1980-01-04 | 105.22  106.52

julia> op[1:3] .- cl[2:4]
2x1 TimeArray{Float64,1} 1980-01-04 to 1980-01-07

            Op.-Cl
1980-01-04 | -1.30
1980-01-07 | -0.29

````
