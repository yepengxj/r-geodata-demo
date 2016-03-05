# r-geodata-demo
library(ggplot2)
library(gpclib)
library(maptools)
library(sp)
# 读取地理信息数据
system("wget http://biogeo.ucdavis.edu/data/gadm2.8/rds/CHN_adm1.rds ")
gadm<-readRDS("/home/rstudio/CHN_adm1.rds")

# 人均水资源量
water <- c(1085,325,1473,3524,1079,2935,3989,2790,4147,358,2046,434
           ,1652,2490,451,3362,1467,871,2145,182,1000,12278,448,377,
           182,1221,3135,152,4976,10000,5298)
# 将数据转为数据框
gpclibPermit()

head(gadm,1)
gadm$NL_NAME_1

china.map <- fortify(gadm,region='ID_1')

head(china.map)

vals <- data.frame(id =order(unique(china.map$id)),val=water)
order(unique(china.map$id))
# 用ggplot命令绘图
ggplot(vals, aes(map_id = id)) + 
  geom_map(aes(fill = val), map =china.map) +
  expand_limits(x = china.map$long, y = china.map$lat) +
  scale_fill_continuous(low = 'red2',high ='yellowgreen',
                        guide = "colorbar")  +
#  opts(title='中国人均年水资源拥有量',
  #       axis.line=theme_blank(),axis.text.x=theme_blank(),
  #       axis.text.y=theme_blank(),axis.ticks=theme_blank(),
  #     axis.title.x=theme_blank(),
  #       axis.title.y=theme_blank()) +
  xlab("") + ylab("")

