// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ripster47

//@version=4
study("Ripster EMA Clouds","Ripster EMA Clouds", overlay=true)
matype = input(title="MA Type", type=input.string, defval="EMA", options=["EMA", "SMA"])

ma_len1 = input(title="Short EMA1 Length", type=input.integer, defval=8)
ma_len2 = input(title="Long EMA1 Length", type=input.integer, defval=9)
ma_len3 = input(title="Short EMA2 Length", type=input.integer, defval=5)
ma_len4 = input(title="Long EMA2 Length", type=input.integer, defval=13)
ma_len5 = input(title="Short EMA3 Length", type=input.integer, defval=34)
ma_len6 = input(title="Long EMA3 Length", type=input.integer, defval=50)
ma_len7 = input(title="Short EMA4 Length", type=input.integer, defval=72)
ma_len8 = input(title="Long EMA4 Length", type=input.integer, defval=89)
ma_len9 = input(title="Short EMA5 Length", type=input.integer, defval=180)
ma_len10 = input(title="Long EMA5 Length", type=input.integer, defval=200)

src = input(title="Source", type=input.source, defval=hl2)
ma_offset = input(title="Offset", type=input.integer, defval=0)
//res = input(title="Resolution", type=resolution, defval="240")

f_ma(malen) =>
    float result = 0
    if (matype == "EMA")
        result := ema(src, malen)
    if (matype == "SMA")
        result := sma(src, malen)
    result
    
htf_ma1 = f_ma(ma_len1)
htf_ma2 = f_ma(ma_len2)
htf_ma3 = f_ma(ma_len3)
htf_ma4 = f_ma(ma_len4)
htf_ma5 = f_ma(ma_len5)
htf_ma6 = f_ma(ma_len6)
htf_ma7 = f_ma(ma_len7)
htf_ma8 = f_ma(ma_len8)
htf_ma9 = f_ma(ma_len9)
htf_ma10 = f_ma(ma_len10)

//plot(out1, color=green, offset=ma_offset)
//plot(out2, color=red, offset=ma_offset)

//lengthshort = input(8, minval = 1, title = "Short EMA Length")
//lengthlong = input(200, minval = 2, title = "Long EMA Length")
//emacloudleading = input(50, minval = 0, title = "Leading Period For EMA Cloud")
//src = input(hl2, title = "Source")
showlong = input(false, title="Show Long Alerts")
showshort = input(false, title="Show Short Alerts")
showLine = input(false, title="Display EMA Line")
ema1 = input(true, title="Show EMA Cloud-1")
ema2 = input(true, title="Show EMA Cloud-2")
ema3 = input(true, title="Show EMA Cloud-3")
ema4 = input(true, title="Show EMA Cloud-4")
ema5 = input(true, title="Show EMA Cloud-5")

emacloudleading = input(0, minval=0, title="Leading Period For EMA Cloud")
mashort1 = htf_ma1
malong1 = htf_ma2
mashort2 = htf_ma3
malong2 = htf_ma4
mashort3 = htf_ma5
malong3 = htf_ma6
mashort4 = htf_ma7
malong4 = htf_ma8
mashort5 = htf_ma9
malong5 = htf_ma10

cloudcolour1 = mashort1 >= malong1 ? #036103 : #880e4f
cloudcolour2 = mashort2 >= malong2 ? #4caf50 : #f44336
cloudcolour3 = mashort3 >= malong3 ? #2196f3 : #ffb74d
cloudcolour4 = mashort4 >= malong4 ? #009688 : #f06292
cloudcolour5 = mashort5 >= malong5 ? #05bed5 : #e65100
//03abc1

mashortcolor1 = mashort1 >= mashort1[1] ? color.olive : color.maroon
mashortcolor2 = mashort2 >= mashort2[1] ? color.olive : color.maroon
mashortcolor3 = mashort3 >= mashort3[1] ? color.olive : color.maroon
mashortcolor4 = mashort4 >= mashort4[1] ? color.olive : color.maroon
mashortcolor5 = mashort5 >= mashort5[1] ? color.olive : color.maroon


mashortline1 = plot(ema1 ? mashort1 : na, color=showLine ? mashortcolor1 : na, linewidth=1, offset=emacloudleading, title="Short Leading EMA1")
mashortline2 = plot(ema2 ? mashort2 : na, color=showLine ? mashortcolor2 : na, linewidth=1, offset=emacloudleading, title="Short Leading EMA2")
mashortline3 = plot(ema3 ?mashort3 : na, color=showLine ? mashortcolor3 : na, linewidth=1, offset=emacloudleading, title="Short Leading EMA3")
mashortline4 = plot(ema4 ? mashort4 :na , color=showLine ? mashortcolor4 : na, linewidth=1, offset=emacloudleading, title="Short Leading EMA4")
mashortline5 = plot(ema5 ? mashort5 : na, color=showLine ? mashortcolor5 : na, linewidth=1, offset=emacloudleading, title="Short Leading EMA5")

malongcolor1 = malong1 >= malong1[1] ? color.green : color.red
malongcolor2 = malong2 >= malong2[1] ? color.green : color.red
malongcolor3 = malong3 >= malong3[1] ? color.green : color.red
malongcolor4 = malong4 >= malong4[1] ? color.green : color.red
malongcolor5 = malong5 >= malong5[1] ? color.green : color.red

malongline1 = plot(ema1 ? malong1 : na, color=showLine ? malongcolor1 : na, linewidth=3, offset=emacloudleading, title="Long Leading EMA1")
malongline2 = plot(ema2 ? malong2 : na, color=showLine ? malongcolor2 : na, linewidth=3, offset=emacloudleading, title="Long Leading EMA2")
malongline3 = plot(ema3 ? malong3 : na, color=showLine ? malongcolor3 : na, linewidth=3, offset=emacloudleading, title="Long Leading EMA3")
malongline4 = plot(ema4 ? malong4 : na, color=showLine ? malongcolor4 : na, linewidth=3, offset=emacloudleading, title="Long Leading EMA4")
malongline5 = plot(ema5 ? malong5 : na, color=showLine ? malongcolor5 : na, linewidth=3, offset=emacloudleading, title="Long Leading EMA5")

fill(mashortline1, malongline1, color=cloudcolour1, transp=45, title="MA Cloud1")
fill(mashortline2, malongline2, color=cloudcolour2, transp=65, title="MA Cloud2")
fill(mashortline3, malongline3, color=cloudcolour3, transp=70, title="MA Cloud3")
fill(mashortline4, malongline4, color=cloudcolour4, transp=65, title="MA Cloud4")
fill(mashortline5, malongline5, color=cloudcolour5, transp=65, title="MA Cloud5")
