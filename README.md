# Th2En & Th2Zh: The large-scale datasets for Thai text cross-lingual summarization | Thai-to-{English, Chinese}
## Introduction 
Thai language remains unexplored in cross-lingual summarization task due to the lack of data. Thus, we constructed two cross-lingual summarization datasets namely Thai-to-Chinese (Th2Zh) and Thai-to-English (Th2En) from TR-TPBS dataset using machine translation services.   
![xsum-example]( https://raw.githubusercontent.com/nakhunchumpolsathien/TH2EN-TH2ZH-Crosslingual-Summariztion-Datasets/master/sxum-gif.gif)
> Example of cross-lingual summarization where output summary is in different from its source document. 
## Dataset Construction
We used [TR-TPBS]( https://github.com/nakhunchumpolsathien/TR-TPBS), a large-scale monolingual Thai text summarization dataset, as source dataset to create cross-lingual summarization datasets. In the same way as [Zhu, et al.]( https://arxiv.org/abs/1909.00156), we constructed Th2En and Th2Zh by translating the summary references into target languages using translation service and filtered out those poorly-translated summaries using round-trip translation technique (RTT). Please refer to the corresponding paper for more details on RTT.
![data-constr](https://raw.githubusercontent.com/nakhunchumpolsathien/TH2EN-TH2ZH-Crosslingual-Summariztion-Datasets/master/data-constr.gif)
> The overview of  Th2En & Th2Zh dataset construction inspired by [Zhu, et al.]( https://arxiv.org/abs/1909.00156)
## Dataset Property
Filtered datasets refer to dataset that are filtered out by RTT strategy.  Full datasets refer to dataset that haven’t been filtered out by RTT strategy. Therefore, full datasets are more noisy but bigger in size. However, interestingly, models trained on full datasets outperform models trained on filter dataset significantly on both Th2En and Th2Zh.  Thus, full datasets are highly recommended.  By setting 𝑇1 and 𝑇2 equal to 0.45 and 0.60 respectively, backtranslation technique filtered out 27.98% from Th2En and 56.79% documents from Th2Zh.
### Filtered datasets 
| | Th2En | Th2Zh | |
| :---| :---: | :---: | :---: |
| Dataset Size | 223,927 |  134,366 | articles |
|Average Thai Article Length | 429.9 | 413  |words |
|Average Translated Summary Length  |37.6 | 35.7  | words |
|Total Unique Thai Words Occurring > 10 times |57,208 |46,588 |words |
|Total Unique Target Words Occurring > 10 times| 27,173| 15,541 | words |
### Full datasets
| | Th2En | Th2Zh | |
| :---| :---: | :---: | :---: |
| Dataset Size | 310,926|  310,926 | articles |

## Experimental Results
###  Performance of cross-lingual summarization models 
Note that end-to-end models are trained on filtered datasets. We use ROUGE-F1 and BertScore-F1 (on abstractive models) to report performance scores on test set. ETrans refers to early translation pipeline (translate-then-summarize). LTrans refers to late translation pipeline (summarize-then-translate). Both traditional pipeline methods suffer from error propagation. 

<table class=MsoTableGrid border=1 cellspacing=0 cellpadding=0
 style='border-collapse:collapse;border:none;mso-border-alt:solid windowtext .5pt;
 mso-yfti-tbllook:1184;mso-padding-alt:0in 5.4pt 0in 5.4pt'>
 <tr style='mso-yfti-irow:0;mso-yfti-firstrow:yes;height:19.85pt'>
  <td width=198 rowspan=3 style='width:148.85pt;border:solid windowtext 1.0pt;
  border-left:none;mso-border-top-alt:solid windowtext .5pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;padding:
  0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><a name=tb51><b>Model</b></a><b><o:p></o:p></b></p>
  </td>
  <td width=218 colspan=4 style='width:163.7pt;border-top:solid windowtext 1.0pt;
  border-left:none;border-bottom:none;border-right:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>Thai to English<o:p></o:p></b></p>
  </td>
  <td width=210 colspan=4 style='width:157.35pt;border:none;border-top:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>Thai to Chinese<o:p></o:p></b></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:1;height:19.85pt'>
  <td width=162 colspan=3 style='width:121.2pt;border:solid windowtext 1.0pt;
  border-left:none;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>ROUGE<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>Bert<o:p></o:p></p>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>Score<o:p></o:p></p>
  </td>
  <td width=162 colspan=3 style='width:121.2pt;border:solid windowtext 1.0pt;
  border-left:none;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>ROUGE<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:solid windowtext 1.0pt;border-left:
  none;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>Bert<o:p></o:p></p>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>Score<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:2;height:19.85pt'>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>R1<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>R2<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>RL<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>F1<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>R1<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>R2<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>RL<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>F1<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:3;height:19.85pt'>
  <td width=627 colspan=9 style='width:469.9pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><i><span
  style='color:black;mso-color-alt:windowtext'>Traditional Approaches</span><o:p></o:p></i></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:4;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>Translated
  Headline <o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>23.44<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>6.99<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>21.49<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>21.55<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>4.66<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>18.58<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:5;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>ETrans -&gt;
  Lead-2<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>51.96<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>42.15<o:p></o:p></b></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>50.01<o:p></o:p></b></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>44.18<o:p></o:p></b></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>18.83<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>43.84</b><b><span lang=TH style='font-size:14.0pt;
  mso-ansi-font-size:11.0pt;line-height:107%;font-family:"Cordia New",sans-serif;
  mso-ascii-font-family:Calibri;mso-ascii-theme-font:minor-latin;mso-hansi-font-family:
  Calibri;mso-hansi-theme-font:minor-latin;mso-bidi-theme-font:minor-bidi'><o:p></o:p></span></b></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:6;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>ETrans -&gt;
  BertSumExt <o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>51.85<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>38.09<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>49.50<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>34.58<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>14.98<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>34.27<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:7;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>ETrans -&gt;
  BertSumExtAbs <o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>52.63<o:p></o:p></b></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>32.19<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>48.14<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><b>88.18<o:p></o:p></b></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>35.63<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>16.02<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>35.36<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>70.42<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:8;height:19.85pt'>
  <td width=198 style='width:148.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>BertSumExt <span
  style='mso-spacerun:yes'> </span>-&gt; LTrans<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>42.33<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>27.33<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>34.85<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>28.11<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>11.85<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>27.46<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>-<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:9;height:19.85pt'>
  <td width=627 colspan=9 style='width:469.9pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><i><span
  style='color:black;mso-color-alt:windowtext'>End-to-End Training Approaches </span><o:p></o:p></i></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:10;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>TNCLS <o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>26.48<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>6.65<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>21.66<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>85.03<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>27.09<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>6.69<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>21.99<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>63.72<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:11;height:19.85pt'>
  <td width=198 style='width:148.85pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>CLS+MS<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>38.28<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>15.21<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>34.68<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>87.22<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>34.34<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>12.23<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>28.80<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>67.39<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:12;height:19.85pt'>
  <td width=198 style='width:148.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'>CLS+MT<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'><u>42.85<o:p></o:p></u></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>19.47<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>39.48<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>88.06<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>42.48<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>19.10<o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>37.73<o:p></o:p></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal align=center style='margin-bottom:8.0pt;text-align:center;
  line-height:107%'>71.01<o:p></o:p></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:13;mso-yfti-lastrow:yes;height:19.85pt'>
  <td width=198 style='width:148.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  background:white;mso-background-themecolor:background1;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><span
  lang=EN-GB style='color:black;mso-color-alt:windowtext;mso-ansi-language:
  EN-GB'>CLS+MT+DIS</span><span lang=EN-GB style='mso-ansi-language:EN-GB'><o:p></o:p></span></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:white;mso-background-themecolor:
  background1;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><span
  style='color:black;mso-color-alt:windowtext'>42.82</span><o:p></o:p></p>
  </td>
  <td width=57 style='width:42.5pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:white;mso-background-themecolor:
  background1;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><u><span
  style='color:black;mso-color-alt:windowtext'>19.62</span><o:p></o:p></u></p>
  </td>
  <td width=57 style='width:42.55pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  background:white;mso-background-themecolor:background1;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><u><span
  style='color:black;mso-color-alt:windowtext'>39.53</span><o:p></o:p></u></p>
  </td>
  <td width=57 style='width:42.5pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;background:white;mso-background-themecolor:background1;
  padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><span
  style='color:black;mso-color-alt:windowtext'>88.03</span><o:p></o:p></p>
  </td>
  <td width=57 style='width:42.55pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:white;mso-background-themecolor:
  background1;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><u><span
  style='color:black;mso-color-alt:windowtext'>43.20</span><o:p></o:p></u></p>
  </td>
  <td width=48 style='width:36.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:white;mso-background-themecolor:
  background1;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><b><u><span
  style='color:black;mso-color-alt:windowtext'>19.19</span><o:p></o:p></u></b></p>
  </td>
  <td width=57 style='width:42.5pt;border:solid windowtext 1.0pt;border-top:
  none;mso-border-top-alt:solid windowtext .5pt;mso-border-alt:solid windowtext .5pt;
  background:white;mso-background-themecolor:background1;padding:0in 5.4pt 0in 5.4pt;
  height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><u><span
  style='color:black;mso-color-alt:windowtext'>38.52</span><o:p></o:p></u></p>
  </td>
  <td width=48 style='width:36.15pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;background:white;mso-background-themecolor:
  background1;padding:0in 5.4pt 0in 5.4pt;height:19.85pt'>
  <p class=MsoNormal style='margin-bottom:8.0pt;line-height:107%'><b><u><span
  style='color:black;mso-color-alt:windowtext'>72.19</span><o:p></o:p></u></b></p>
  </td>
 </tr>
</table>

### Influence of back-translation (RTT) 
We conduct an experiment to investigate the effectiveness of back-translation by training all end-to-end models on both full datasets and filtered datasets. The below table shows ROUGE-F1 scores of the models trained on filtered datasets and full datasets. 
<table class=MsoTableGrid border=1 cellspacing=0 cellpadding=0 width=627
 style='margin-left:-9.0pt;border-collapse:collapse;mso-table-layout-alt:fixed;
 border:none;mso-border-alt:solid windowtext .5pt;mso-yfti-tbllook:1184;
 mso-padding-alt:0in 5.4pt 0in 5.4pt'>
 <tr style='mso-yfti-irow:0;mso-yfti-firstrow:yes;height:14.75pt'>
  <td width=72 rowspan=3 style='width:.75in;border:solid windowtext 1.0pt;
  border-left:none;mso-border-top-alt:solid windowtext .5pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;padding:
  0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>Model<o:p></o:p></span></b></p>
  </td>
  <td width=280 colspan=6 style='width:209.7pt;border:solid windowtext 1.0pt;
  border-left:none;mso-border-left-alt:solid windowtext .5pt;mso-border-alt:
  solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:10.0pt'>Thai to English<o:p></o:p></span></b></p>
  </td>
  <td width=275 colspan=7 style='width:206.3pt;border-top:solid windowtext 1.0pt;
  border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
  mso-border-left-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-bottom-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:10.0pt'>Thai to Chinese<o:p></o:p></span></b></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:1;height:14.75pt'>
  <td width=144 colspan=3 style='width:1.5in;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>Full
  Dataset</span></b><b><span lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=136 colspan=3 style='width:101.7pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>Filtered <a name=tb54>Dataset</a><o:p></o:p></span></b></p>
  </td>
  <td width=140 colspan=3 style='width:105.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-alt:solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>Full Dataset</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=135 colspan=4 style='width:101.0pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>Filtered Dataset<o:p></o:p></span></b></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:2;height:14.75pt;mso-row-margin-right:.45pt'>
  <td width=51 style='width:38.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>R1</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.25pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps;color:black;
  mso-color-alt:windowtext'>R2</span></b><b><span lang=EN-GB style='font-size:
  9.0pt;font-variant:small-caps'><o:p></o:p></span></b></p>
  </td>
  <td width=47 style='width:35.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;background:
  #F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:242;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps;color:black;
  mso-color-alt:windowtext'>RL</span></b><b><span lang=EN-GB style='font-size:
  9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=44 style='width:33.05pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>R1<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>R2<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.35pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>RL</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>R1</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps;color:black;
  mso-color-alt:windowtext'>R2</span></b><b><span lang=EN-GB style='font-size:
  9.0pt;font-variant:small-caps'><o:p></o:p></span></b></p>
  </td>
  <td width=49 style='width:36.7pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;mso-border-top-alt:
  solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;background:
  #F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:242;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps;color:black;
  mso-color-alt:windowtext'>RL</span></b><b><span lang=EN-GB style='font-size:
  9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=43 style='width:31.95pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>R1<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>R2<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>RL</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td style='mso-cell-special:placeholder;border:none;padding:0in 0in 0in 0in'
  width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='mso-yfti-irow:3;height:14.75pt;mso-row-margin-right:.45pt'>
  <td width=72 style='width:.75in;border:none;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>TNCLS </span><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></p>
  </td>
  <td width=51 style='width:38.15pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>31.10</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.25pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>9.39</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=47 style='width:35.6pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>26.59</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=44 style='width:33.05pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:dashed windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>27.09<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>6.69<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.35pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>21.99<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>33.15</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>10.89</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=49 style='width:36.7pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-top-alt:solid windowtext .5pt;mso-border-top-alt:solid windowtext .5pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>28.65</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=43 style='width:31.95pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  mso-border-left-alt:dashed windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>26.48<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>6.65<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-top-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>21.66<o:p></o:p></span></p>
  </td>
  <td style='mso-cell-special:placeholder;border:none;padding:0in 0in 0in 0in'
  width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='mso-yfti-irow:4;height:14.75pt;mso-row-margin-right:.45pt'>
  <td width=72 style='width:.75in;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>CLS+MS <o:p></o:p></span></p>
  </td>
  <td width=51 style='width:38.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>41.96</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.25pt;border:none;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>18.48</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=47 style='width:35.6pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>38.58</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=44 style='width:33.05pt;border:none;mso-border-left-alt:dashed windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>38.23<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>15.21<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.35pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>34.68<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>45.72</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>21.92</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=49 style='width:36.7pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>41.39</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=43 style='width:31.95pt;border:none;mso-border-left-alt:dashed windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>34.34<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>12.23<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>28.80<o:p></o:p></span></p>
  </td>
  <td style='mso-cell-special:placeholder;border:none;padding:0in 0in 0in 0in'
  width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='mso-yfti-irow:5;height:14.75pt;mso-row-margin-right:.45pt'>
  <td width=72 style='width:.75in;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;font-variant:small-caps'>CLS+MT</span><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></p>
  </td>
  <td width=51 style='width:38.15pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>42.39</span><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.25pt;border:none;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>18.96</span><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></p>
  </td>
  <td width=47 style='width:35.6pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>39.17</span><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></p>
  </td>
  <td width=44 style='width:33.05pt;border:none;mso-border-left-alt:dashed windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>42.85<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>19.47<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.35pt;border:none;border-right:solid windowtext 1.0pt;
  mso-border-right-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt'>39.48<o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;mso-border-left-alt:solid windowtext .5pt;
  background:#F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:
  242;padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>48.46</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>23.80</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=49 style='width:36.7pt;border:none;border-right:dashed windowtext 1.0pt;
  mso-border-right-alt:dashed windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>44.29</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=43 style='width:31.95pt;border:none;mso-border-left-alt:dashed windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>42.48<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>19.10<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>37.73<o:p></o:p></span></p>
  </td>
  <td style='mso-cell-special:placeholder;border:none;padding:0in 0in 0in 0in'
  width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='mso-yfti-irow:6;mso-yfti-lastrow:yes;height:14.75pt;mso-row-margin-right:
  .45pt'>
  <td width=72 style='width:.75in;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;padding:
  0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>CLS+MT+DIS<o:p></o:p></span></p>
  </td>
  <td width=51 style='width:38.15pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>43.49</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.25pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>20.20</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=47 style='width:35.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;background:
  #F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:242;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>40.21</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=44 style='width:33.05pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:dashed windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>42.68<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>19.29<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.35pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;mso-border-right-alt:solid windowtext .5pt;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>39.40<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:solid windowtext .5pt;mso-border-left-alt:solid windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>48.67</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;background:#F2F2F2;mso-background-themecolor:
  background1;mso-background-themeshade:242;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>24.15</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=49 style='width:36.7pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:dashed windowtext 1.0pt;mso-border-bottom-alt:
  solid windowtext .5pt;mso-border-right-alt:dashed windowtext .5pt;background:
  #F2F2F2;mso-background-themecolor:background1;mso-background-themeshade:242;
  padding:0in 5.4pt 0in 5.4pt;height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><b><span
  lang=EN-GB style='font-size:9.0pt;color:black;mso-color-alt:windowtext'>44.28</span></b><b><span
  lang=EN-GB style='font-size:9.0pt'><o:p></o:p></span></b></p>
  </td>
  <td width=43 style='width:31.95pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-left-alt:dashed windowtext .5pt;mso-border-left-alt:dashed windowtext .5pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>43.20<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal'><span
  lang=EN-GB style='font-size:9.0pt'>19.19<o:p></o:p></span></p>
  </td>
  <td width=46 style='width:34.3pt;border:none;border-bottom:solid windowtext 1.0pt;
  mso-border-bottom-alt:solid windowtext .5pt;padding:0in 5.4pt 0in 5.4pt;
  height:14.75pt'>
  <p class=MsoNormal align=center style='text-align:center;line-height:normal;
  page-break-after:avoid'><span lang=EN-GB style='font-size:9.0pt'>38.52<o:p></o:p></span></p>
  </td>
  <td style='mso-cell-special:placeholder;border:none;padding:0in 0in 0in 0in'
  width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
</table>

TNCLS, CLS+MS and CLS+MT are introduced in this [paper](https://arxiv.org/abs/1909.00156). BertSum models are presented in this [paper](https://arxiv.org/abs/1908.08345). CLS+MT+DIS is proposed in Nakhun’s thesis (unpublished).
## Download Dataset
--coming very soon--
 | Dataset | Remarks | 
| :---| :--- | 
| Th2En | contains ` th2en_full.csv`  and ` th2en_filtered.csv`   | 
| Th2Zh| contains ` th2zh_full.csv`  and ` th2zh_filtered.csv`   |
| test-valid | ` contains th2{en,zh}_test.csv`  and ` th2{en,zh}_valid.csv` . |

Each CSV file contains the following columns: ` th_body` , ` th_sum` , ` {en,zh}_body` , ` {en,zh}_sum` and ` url`. 

## Need trained models for research purpose?
If you would like to obtain trained models (with vocabulary files) as reported in this experiment for research purposes, these models are available per request. Please contact nakhun.chum(at sign)gmail.com.
## Contributors
-	Nakhun Chumpolsathien, School of Computer Science, Beijing Institute of Technology (BIT)
-	Tanachart Arayachutinan, BIT, (Contribution was made during his Master's candidacy at BIT.)
## Acknowledgement
-	These cross-lingual datasets, including TR-TPBS, are parts of Nakhun Chumpolsathien’s master’s thesis at school of computer science, Beijing Institute of Technology. Therefore, as well, a great appreciation goes to his supervisor, Assoc. Prof. Gao Yang.
-	We would like to thank Beijing Engineering Research Center of High Volume Language Information Processing and Cloud Computing Applications for providing computing resources to conduct the experiment.
-	In this experiment, we used PyThaiNLP v. 2.2.4  to tokenize (on both word & sentence levels) Thai texts. For Chinese and English segmentation, we used Stanza. 
-	We used [‘scb-mt-en-th-2020’](https://arxiv.org/abs/2007.03541) dataset to jointly train machine translation loss in CLS+MT and CLS+MT+DIS (Th2En).

## License
Th2En and Th2Zh datasets are licensed under [MIT License]( https://github.com/nakhunchumpolsathien/TH2EN-TH2ZH-Crosslingual-Summariztion-Datasets/blob/master/LICENSE).

