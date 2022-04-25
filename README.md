# grid_legend

```
myborder<-unit(c(0.1,0.5,0.1,0.5),"lines")
symbolvp<-viewport(width=unit(1,"lines"))
frame_curve<-frameGrob()
frame_curve<-packGrob(frame_curve,textGrob("Curve",vp=symbolvp),col=1,row=1,border=myborder)
frame_curve<-packGrob(frame_curve,textGrob("Measure",x=0,just="left"),col=2,row=1,border=myborder)
frame_curve<-packGrob(frame_curve,textGrob("AUC (95% CI)",x=0,just="left"),col=3,row=1,border=myborder)
for(ii in 1:nrow(df_ROC)){
  CI<-ci.auc(df_ROC$roc[[ii]])
  temp<-paste0(
    num_to_str(df_ROC$auc[[ii]],2)," (",
    num_to_str(CI[1],2),", ",
    num_to_str(CI[3],2),")")
  grob1<-linesGrob(x=c(0,1),y=c(0.5,0.5),vp=symbolvp)
  grob2<-textGrob(df_ROC$name[ii],x=0,just="left")
  grob3<-textGrob(temp,x=0,just="left")
  frame_curve<-packGrob(frame_curve,grob1,row=ii+1,col=1,border=myborder)
  frame_curve<-packGrob(frame_curve,grob2,row=ii+1,col=2,border=myborder)
  frame_curve<-packGrob(frame_curve,grob3,row=ii+1,col=3,border=myborder)
}
grid.newpage()
grid.draw(frame_curve)

```
