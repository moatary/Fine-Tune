# Fine-Tune tool for numerical-analysis and machine-learning applications:
Fine-tune huge number of parameters in all modules and functions of your python code simultaenously. 

Also, it is applied to an image-processing preprocessing function which has to fine-tune various edge-detection, convolution-filters and histgram-equalization thresholds to manually improve image-filtering threshold through visualization. (Please refer to the "Examples" directory.

This respository is developed to ease the hyperparameter tuning and debugging difficulties arises when there are multiple parameters in different locations of your code that needs to be fine tuned. In the case of default functions in sklearn, one may use pipeline of functions and pass the pipeline to grid optimizer. But what about tuning variables that are everywhere in any types of class? The interactive feature of Python fascilitates such capability to handle tune all parameters from different sections of your code all at once.


------------------------------- <<< Instruction To Use >>> ----------------------------------

To tune your variables and methods, first import the class "autotuner", then pass all your hypereparameters states through one dict object to the "autotuner" constructor. Example:

    from ../tuner import *   # import tuner class and its requirement
    tunes={ 'batchsampler':['"shuffle"','"normal"'],'negative_sampler_thresh':['0.003','0.001','0.009'] , 'projElossfcnType':['"listwise_sumoverbatch"', '"pointwise"'] } # Variables you've chosen for tuning. Note: Use string from for numbers.
    tunerobj=tuner(tunes) # call the tuner-class constructor
    for args_of_tune in tunerobj:  # iterate over each tune case (i.e., for 3 parameters tuning, each having 3,7,2 cases respectively, iterator iterates over 3*7*2 different cases
        self.dict.update( args_of_tune.dict ) #Now, cast args.dict to dict of current scope. For other adding approach, please refer to next paragraph.   
        ##As the variable names , You are free to do whatever you wnat on the tuned variables. Just call them... The next two lines are ARBITRARY!
        args= prompt4args(the_variable_names_you_tuned) # function where u're free to define all dataset infos and what to out.
        model.forward(new_variables, args_of_tune, etc...) # now you can pass your resulted data to whereever you want, ex., machine learning model.


--------------------------- Tuning parameters by using "exec" function--------------------------

    from ../tuner import *   # import tuner class and its requirement
    tunes={ 'batchsampler':['"shuffle"','"normal"'],'negative_sampler_thresh':['0.003','0.001','0.009'] , 'projElossfcnType':['"listwise_sumoverbatch"', '"pointwise"'] } # Variables you've chosen for tuning. Note: Use string from for numbers.
    tunerobj=tuner(tunes) # call the tuner-class constructor
    for args_of_tune in tunerobj:  # iterate over each tune case (i.e., for 3 parameters tuning, each having 3,7,2 cases respectively, iterator iterates over 3*7*2 different cases.
        for itmname,itmvalue in zip(tuner.tune.keys(),tuner.tune.values()):
            exec(itmname+'='+itmvalue)
    ##Now use the items you tuned





_____________________ Using tuner for comparing different filtering parameters in image-processing ._______________
The "Example" directory, visualizes different parameter cases of gaussian filter and sobel detector.
As an example of filtering a cat image, the results are shown by this code:

    function1_in_pipeline=  sk.filters.gaussian # note: 1st input is always image, from 2nd input to end, one must be assigned as 'tune' input.
    Input_Image_to_tune= img
    pipeline= [function1_in_pipeline]#, function2_in_pipeline]
    inputs_to_eachfunc_assign_inputs2gettuned =[['tune'] ] # each function may only have one tuning variable or zero, assigned by mentioning 'tune'. Other values are only assigned as its initial value.
    each_tuning_param_values=[[8,9,10,12,20,30,35,40,50,70,75,80,90,100]]#, [3,4,5,6,7,8,9]] # [8,10,12,20,30,35,40] for gaussian filter tuning , and [1,2,3,4] for sobel function.
    comparetunes(Input_Image_to_tune, pipeline, inputs_to_eachfunc_assign_inputs2gettuned, each_tuning_param_values)

![GitHub Logo](/Example/Figure_1.png)
Format: ![Alt Text](url)


The main cat image was:
![GitHub Logo](/Example/cat.jpg)
Format: ![Alt Text](url)
