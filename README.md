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
The following features can be used to predict solar output:
- Horizontal Irradiance
- Humidity
- Temperature
- Wind Speed
- Wind Direction
- Cloud Cover
- Precipitation
- Pressure
- Solar Zenith Angle
- Solar Azimuth Angle
- Solar Altitude Angle
- Solar Declination Angle
- Etc.

## Configurable prediction horizon

## References
See:

- [Multi-time-horizon Solar Forecasting Using Recurrent Neural Network](https://arxiv.org/abs/1807.05459)
- [Awesome Energy Forecasting](https://github.com/cuge1995/awesome-energy-forecasting)


