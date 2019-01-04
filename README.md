Linear Regression 
===================

- Data set Used: HW4GaussianClustersData (Please look in DATA folder)

Question 1
------------

- Plot the data on a 2-D scatter plot and mark by hand the boundaries of the ideal clusters that you would like discovered in this dataset. 		
  
  ![image](../master/2a.png)
   
  
  ```
   while(flag=='T'):    
    print(count+1,"- feature Regression Models","\n")
    count=count+1
    counter=0
    i_vector=[]
    aic_value=[]  
    lmwhite=[]
    for i in df.columns:
        if i=="quality" or feature.find(i)>0:
            continue;
        if feature=="" :
            lmwhite_dummy=smf.ols(formula='quality~'+ i,data=df).fit()
        else :
            lmwhite_dummy=smf.ols(formula='quality~ '+feature+"+"+ i ,data=df).fit()
        i_vector.append(feature+ "+"+i)    
        lmwhite.append(lmwhite_dummy)
        r2_value_dummy=(lmwhite_dummy.rsquared)
        r2_value.append(r2_value_dummy)
        aic_value_dummy=(lmwhite_dummy.aic)
        aic_value.append(aic_value_dummy)
        print("Model:: ","Feature:",(feature+ "+"+i).strip("+"),"R2_Value:",
              round(r2_value_dummy,4),"AIC_Value:",round(aic_value_dummy,6),"\n") 
    
    i_vec.append(i_vector)
    aic.append(aic_value)
    r2.append(r2_value)
    feature_num = r2_value.index(max(r2_value))
    feature=i_vector[feature_num]
    print("Best Feature with highest r2 value:",feature.strip("+"),"R2_Value : ",
          round(r2_value[feature_num],4),"AIC_Value:",round(aic_value[feature_num],6),"\n")
    r2_value=[]
    best_aic.append(aic_value[feature_num])  
    bestlm.append(lmwhite[feature_num])
    
    # Stopping Condition
    for j in aic_value:
        if j>=best_aic[-2]:
            counter=counter+1  
        if counter==len(aic_value)-1:
            flag='F'
  ```

 Question 2
------------ 
- Report the features included, their coefficients, and p-values for the coefficients in the best model found above. Comment on the magnitudes of the p-values.  

  >8- Feature Regression model best fitting to the data with optimal R2 and AIC value is:
  >Best Feature with highest r2 value: alcohol+volatile_acidity+residual_sugar+free_sulfur_dioxide+density+pH+sulphates+fixed_acidity R2_Value: 0.2818 AIC_Value: 11106.287754
  
  P_Value:  The p-values for the coefficients indicate whether these relationships are statistically significant. 
            Along with the coefficients, p values provide enough evidence to reject the otherwise taken null hypothesis instead of the regression line obtained.
			
        A higher Pvalue indicate that the variable is not significant for the regression model, whereas a lower magnitude 
		provides enough evidence that the inclusion of the variable is significant for the regression model and that the target value is dependent on the variable.
		
  ![hyperlink](p Values Explained):http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-interpret-regression-analysis-results-p-values-and-coefficients 
    
	In our model all the pvalues are almost equal to 0.00 which means that they are all very much significant in regression model and contribute in the prediction.

 Question 3
------------ 	
-Find the five wines that have the largest magnitudes of difference between the predicted and the actual wine-quality values. Look at the regression model, the rest of the data, and comment on why you think these wines are outliers.
 
 #Fitting the obtained Regression line on the data to predict the value:
	
	```
	  pred=bestlm[7].predict(X_Val)
	  error=abs(pred)
	```
  
  The quality groups of 3,9 are only 25 among the 4898. The very little proportion of these stay as the outliers providing very little learning data for the regression models. 
  If the model is fitted to include these as well, it would lead to overfitting of the data.


	