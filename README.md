def readFile(fn):
  """ reading the file"""
  df = pd.read_csv(fn)
  countrydf = df.iloc[:,0:1]
  yeardf = df.iloc[:,1:]
  return countrydf, yeardf # returns country and year data frames


def displaydf(cdf, ydf):
  """ Displaying the Country and year dataframes"""
  print("Country Dataframe")
  display(cdf)
  print("\nYear Dataframe")
  display(ydf)

def statisticsdata(cdf,ydf):
  """ Computing the statistical properties of the data"""
  countrylist = cdf['Country Name'].tolist()
  stat = ydf.apply(pd.DataFrame.describe, axis=1)
  stat.insert(0, 'Countries', countrylist)
  print('\nStatistics Data')
  display(stat)
  print("\n\n")

def line_plot(cdf,ydf):
  """ Plotting the line plot for the data"""
  years = [i for i in ydf]
  l=[]
  for i in range(len(ydf['1985'])):
    d = ydf.loc[ydf['1985']==ydf['1985'][i]].values.flatten().tolist()
    l.append(d)
    d = []
  countries = cdf['Country Name'].tolist()
  plt.figure(figsize=[10,10])
  for i in range(10):
    plt.plot(years,l[i],marker=".",mec="r",mfc="r", label = countries[i])
  plt.legend()
  plt.xlabel('Year')
  plt.ylabel('Agricultural Land in sq km')
  plt.title("Agricultural Land different Countries in sq km", size = 20)
  plt.show()
  plt.close()

def heatMap():
  """ Drawing the correlation plot for the country JAPAN"""
  fn = pd.read_csv('/content/Japan.csv')
  c = fn.corr()
  plt.title("Correlation between few indicators for Japan\n\n")
  display(c)

""" importing the libraries"""
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

filename = "/content/agriculture.csv"
countrydf, yeardf = readFile(filename)
displaydf(countrydf, yeardf)
statisticsdata(countrydf, yeardf)
line_plot(countrydf, yeardf)
heatMap()
