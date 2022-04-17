# HA Solar Forecasting

## What's the purpose of this project?
The purpose of this project is to provide a simple way to forecast solar energy production for your [Home Assistant](https://home-assistant.io/) installation using a minimal and ideally zero set of cloud API's. 

## Why is this needed?
There are atleast two addons that I know of that provide solar forecasting information, [SolCast](https://github.com/oziee/ha-solcast-solar) and [forecast.solar](https://www.home-assistant.io/integrations/forecast_solar/). Of these two, SolCast seems to be the most accurate. However, it does not have a native integration and it's free API has a very limited amount of calls. I have also tried forecast.solar and found it's accuracy is severely lacking. 

On top of this there is no guarantee that forecast.solar will remain operational in the future, as is the case with any cloud service. An increasing dependence on renewebles also means an increasing dependence on services that provide vital data to your home. I would like to schedule my heavy electricity consumers such that I maximize the utility of my solar panels, doing so at the optimal time every day may save me hundreds of euros on a yearly basis, especially at these energy prices.

For example: 
- Charging an electric car 
- Powering the washing machine

So in the true spirit of Home Assistant, we want to have solar forecasting with maximum locality and accuracy and as little reliance on cloud services as possible. 

## What's local forecasting?
Local forecasting means that the logic to predict solar panel output resides on the Home Assistant server. 

## Featureset
The following features can be used to predict solar output, see also [1]:
- Downwelling global solar (Watts/m^2)
- Upwelling global solar (Watts/ m^2)
- Directnormal solar (Watts/ m^2)
- Downwelling diffuse solar (Watts/m^2)
- Downwelling thermal infrared (Watts/ m^2)
- Downwelling IR case temp. (K) 
- Downwelling IR dome temp. (K) 
- Upwelling thermal infrared (Watts/ m^2)
- Upwelling IR case temp. (K)
- Upwelling IR dome temp. (K)
- Global UVB (milliWatts/ m^2)
- photosynthetically active radiation (Watts/m^2) 
- Net solar (dw_solar - uw_solar) (Watts/ m^2)
- Net infrared (dw_ir - uw_ir) (Watts/ m^2)
- Net radiation (netsolar+netir) (Watts/ m^2)
- 10-meter air temperature (C)
- Relative humidity (%)
- Wind speed (ms^1)
- Wind direction (degrees, clockwise from north)
- Station pressure (mb)

On top of this, we can use the featureset available from the solar installation itself. The most important feature is the solar panel output in watts. This will be used to train the time series model and also serve as a baseline for the prediction.

## Configurable prediction horizon

## Setup
Currently, my vision is as follows:
- A user has a solar installation with historical data, preferably detailed data over 1 or more years
- If detailed data is not available, the model will be less accurate but it should still be possible to use it
- This data should be available in a CSV file, which can be aquired from a database like influxDB
- It will be difficult to get accurate timeseries weather data without a cloud service
- The ideal solution would only use a weather station in your garden that collects relevant data

## References
See:

- [1] [Multi-time-horizon Solar Forecasting Using Recurrent Neural Network](https://arxiv.org/abs/1807.05459)
- [2] [Awesome Energy Forecasting](https://github.com/cuge1995/awesome-energy-forecasting)
- [3] [Photovoltaic system derived data for determining the solar resource and
for modeling the performance of other photovoltaic systems](https://isiarticles.com/bundles/Article/pre/pdf/138552.pdf)


