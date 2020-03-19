Review HTF sections 7.10 and 7.11

Consider a 1-nearest neighbor classifier applied to a two-class
classification problem, where the marginal probability associated with
either class is one half, and where the distribution of a univariate
predictor is standard normal, independent of class (i.e., not a very
good predictor). Do the following:

1.  Show that the expected prediction error (EPE; HTF expression 7.3) is
    equal to 0.5.

<!-- -->

    set.seed(10)
    n <- 900
    x <- rnorm(n)
    y <- rbinom(1,n = n, prob = 0.5)

    # Using the same training data each time
    data <- data.frame(x,y)


    one_nn <- function(data){
      test <-data.frame(x = rnorm(100), y = rbinom(1,n = 100, prob = 0.5))
      test$preds <- knn(train = data.frame(data$x), test = data.frame(test$x), cl = rbinom(1,n = n,prob = 0.5))
      
      # prediction error
      err_tau <- length(which(test$y == test$preds))/nrow(test)
      return(err_tau)
    }

    results <- replicate(10000, one_nn(data))

    # expected prediction error
    (err1 <- mean(results))

    ## [1] 0.500211

These results indicate that the expected prediction error is
approximately 1/2.

1.  Show that $E\_z\[\\hat{Err}\_{boot}\]$ (expectation of HTF
    expression 7.54) is approximately equal to 0.184, where z represents
    the training sample of N class and predictor pairs. Thus,
    demonstrate that the bootstrap estimate of EPE is optimistic.

I will again show this by simulation. I am assuming zero-one loss.

    ## From class notes
    zero_one_loss <- function(y, pred)
      ifelse(y == pred, 0, 1) 

    ## compute error
    error <- function(data, fit, loss=zero_one_loss) {
      pred <-predict(fit, data) 
      mean(loss(data$y, pred))
    }

    err_boot <- function(kNN = 1, B=1000) {
        err<- NULL
        for(i in 1:B){
          
        ## resample the data
        data_boo <- data[sample(nrow(data), replace=T),]
     
        ## fit kNN model to resamples training data
        knn_fit <- knnreg(y ~ x, k=kNN, data=data_boo)
        
        ## keep track of each error for each bootstrap sample
        ## error calculated using full original data 
        err<- c(err,error(data = data,fit = knn_fit, loss= zero_one_loss))
        
    }
      return(c(mean(err),sd(err)))
    }


    results2 <- err_boot(kNN = 1, B = 10000)
    (err2 <- results2[1])

    ## [1] 0.1877682

We see that the expression is approximately equal to 0.184.

1.  Compute or approximate $E\_z\[\\hat{Err}^{(1)}\]$ (expectation of
    HTF expression 7.56).

    I will approximate this value by simulation.

<!-- -->

    ## From class notes
    zero_one_loss <- function(y, pred)
      ifelse(y == pred, 0, 1) 

    ## compute error
    error <- function(data, fit, loss=zero_one_loss) {
      pred <-predict(fit, data) 
      mean(loss(data$y, pred))
    }

    err_boot <- function(kNN = 1, B=1000) {
    err<- NULL
        for(i in 1:B){
          
        ## resample the data
        ind_boo <- sample(nrow(data),replace = TRUE)  
        data_boo <- data[ind_boo,]
        
     
        ## fit kNN model to resample data data
        knn_fit <- knnreg(y ~ x, k=kNN, data=data_boo)
        
        ## keep track of each error for each bootstrap sample
        ## calculate error using data not in resample
        err <- c(err,error(data = data[-ind_boo,],fit = knn_fit, loss= zero_one_loss))
        
    }
      return(c(mean(err),sd(err)))
    }

    results3 <- err_boot(kNN = 1, B = 10000)
    (err3 <- results3[1])

    ## [1] 0.5106715

We see that the expectation of HTF expression 7.56 is approximately 0.5,
but appears to have a slight upward bias.

1.  Compute or approximate $E\_z\\left\[\\hat{Err}^{(0.632)}\\right\]$
    (expectation of HTF expression 7.57).

I will compute this mathematically.

$$
\\begin{align\*}
E\_z\[\\hat{Err}^{(0.632)}\]  &= E\_z\\left\[0.368 \\times \\bar{err} + 0.632 \\times \\hat{Err}^{(1)}\\right\] \\\\
&=  0.368 \\times E\_z\\left\[\\bar{err}\\right\] + 0.632 \\times E\_z\\left\[\\hat{Err}^{(1)}\\right\]\\\\
&=  0.368 \\times \\bar{err} + 0.632 \\times E\_z\\left\[\\hat{Err}^{(1)}\\right\]\\\\
&=  0.368 \\times 0 + 0.632 \\times 0.5\\\\
&= 0.316
\\end{align\*}
$$
