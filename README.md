# HA Solar Forecasting

## What's the purpose of this project?

The purpose of this project is to provide a simple way to forecast solar energy production for your [Home Assistant](https://home-assistant.io/) installation using a minimal (and ideally zero) set of cloud API's.

## Why is this needed?

There are atleast two addons that I know of that provide solar forecasting information, [SolCast](https://github.com/oziee/ha-solcast-solar) and [forecast.solar](https://www.home-assistant.io/integrations/forecast_solar/). Of these two SolCast seems to be the most accurate. However, it does not have a native integration and its free API supports only a very limited amount of calls per day. I have also tried forecast.solar and found its accuracy is severely lacking, the mean error is too high to support time sensitive applications.

![forecast_solar_bad](https://user-images.githubusercontent.com/37669773/177314734-06e50bbc-861a-45d5-889e-f0ab3490c899.png)

On top of this there is no guarantee that forecast.solar will remain operational in the future, as is the case with any (and especially free) cloud service. As the electricity grid moves away from fossil fuels the dependency on intermittent renewables increases. Usage of these new and unreliable electricity sources also means an increasing dependency on services that provide critical data. This data can be used to schedule your home appliances during peak solar hours in order to maximize available solar energy self consumption, leading to lower carbon emissions and a lower energy bill. I would like to schedule my heavy electricity consumers such that I maximize the utility of my solar panels, doing so at the optimal time every day may save me hundreds of euros on a yearly basis, especially at current energy rates.

Examples include:

- Charging an electric car
- Powering the washing machine

So in the true spirit of Home Assistant, we want to have solar forecasting with maximum locality and accuracy and as little reliance on cloud services as possible.

## What's local forecasting?

Local forecasting means that the logic to predict solar panel output resides on the Home Assistant server. 

## Featureset

The following features can be used to predict solar output, see also [1] and [4]:

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

## On-line learning
We can make it possible to continuously improve the model by enabling on-line learning. We can have a 'very well' trained model that we train in the cloud on GPU's. This model can then continue to train once deployed. The training will happen by feeding in the solar site data and updating the model's parameters accordingly. This should yield superior performance. 

## Setup

- A user has a solar installation with historical data of about 2 days, preferable at interval of 30 seconds. 
- The ideal setup would use a weather station situated in your garden to provide the model with the necessary atmospheric and meteorological data. 
- To predict solar output, we input timeseries data into the model and output a prediction for the next time step(s).   

## Retrieve data from InfluxDB

First, SSH into the influxDB docker container.

The following SQL command can then be used to retrieve solarpanel data from InfluxDB:

`curl -G 'http://localhost:8086/query' --data-urlencode "db=home_assistant" --data-urlencode "q=SELECT * FROM "W" WHERE ("entity_id" = 'solaredgemb_ac_power')" -H "Accept: application/csv" >  home_assistant.csv`

Then run:
`mv /home_assistant.csv /var/lib/influxdb/`

To move the file to the shared volume.

## References

See:

- [1] [Multi-time-horizon Solar Forecasting Using Recurrent Neural Network](https://arxiv.org/abs/1807.05459)
- [2] [Awesome Energy Forecasting](https://github.com/cuge1995/awesome-energy-forecasting)
- [3] [Photovoltaic system derived data for determining the solar resource and
for modeling the performance of other photovoltaic systems](https://isiarticles.com/bundles/Article/pre/pdf/138552.pdf)
- [4] [PVoutput](https://pvoutput.org/)
- [5] [LSTM explanation](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [6] [Multi Step Time Series Forecasting](https://machinelearningmastery.com/multi-step-time-series-forecasting/)
- [7] [nvidia time series](https://www.kaggle.com/code/anmolgupta11090/jpx-tokyo-stock-prediction-with-nvidia-tspp/notebook?ncid=so-link-274481-vt27&=&linkId=100000132389550#cid=an01_so-link_en-us)


