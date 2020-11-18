# ada-logit

## Feedback

You *do* interpret some probabilities, but there's no obvious work shown, so I can't really tell if your interpretation is 
correct. Did you do the trick of predicting probabilities and is that what you're reporting? I kind of doubt it, but 
only because I can't see any code that does this. 

I ask you to interpret the coefficients for the clients. The "dummy" category is Bulldog Tours, 
which is the first client alphabetically. It's estimate is included in the intercept. At the 
very least, you should interpret the coefficients of the clients in your table. Exponentiate the
estimates to get odds multipliers. 

If you wanted to do a more thorough job of it, one easy way to get probability estimates
is to create a new data set. Your model has the client term, total spent, bookings in 13 to 
26 months, and mean leading days.

You could do something like this to get a new data set:
```
new.d <- tibble(client_fct = unique(d$client_fct),
                total_spent = median(d$total_spent,na.rm=T),
                bookings_in_13_to_26_months = median(d$bookings_in_13_to_26_months,na.rm=T),
                mean_leading_days = median(d$mean_leading_days,na.rm=T))
				
new.d <- new.d %>% 
	mutate(pred_prob = predict(glm.1,newdata=new.d,type="response")) %>% 
	arrange(pred_prob)
				
```

With `type` set to "response", the predictions will be probabilities. You can look at 
the data frame `new.d` to get an estimate of the probability of rebooking as the 
clients change. 

Please revise.


