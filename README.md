# Text_Summerization

Steps to run the pertained model on the dataset

1). Download the finished dataset from the link shared by Narayana sir.
    So here is the direct link where i have mentioned the link from where i have downloaded the final prepared data which will be used by us
    
https://github.com/abisee/cnn-dailymail

Below is the image of the description where it is mentioned that we have to use the finished_files/chunked


Screen Shot 2019-07-26 at 1.44.42 PM.png
    
2). The model which is shared in the above link is based on python 2 so in our case we need to use the python 3 based model..which I downloaded from 

https://github.com/becxer/pointer-generator/

There are modification which I did on it.So attaching the zip folder for that so that you guys can use it straight away.	
3). You need to download the retrained model from 
https://drive.google.com/file/d/0B7pQmm-OfDv7ZUhHZm9ZWEZidDg/view

Please remember there are 2 retrained models which are available …The above link has model which is based on tensor-flow 1.2.1..there are few deprecated api’s but it will work.

4). Download the finished_files from the below link 
https://drive.google.com/file/d/0BzQ6rtO2VN95a0c3TlZCWkl3aU0/view?usp=sharing

It is mentioned at the https://github.com/JafferWilson/Process-Data-of-CNN-DailyMail
Screen Shot 2019-07-26 at 2.44.42 PM.png


The link which is mentioned in the last of the above image is the link from where we can download the preprocessed data.

Now keep all the folders in the same place.

Then go in to pointer-generator folder and then run the below command 


python run_summarization.py --mode=decode --data_path=/Users/rajeshjain/projects/GreatLearnings/assignments/residency/gurgaonbatch-rajeshcjain/CapstonProject/finished_files/chunked/val_* --vocab_path=/Users/rajeshjain/projects/GreatLearnings/assignments/residency/gurgaonbatch-rajeshcjain/CapstonProject/finished_files/vocab --log_root=/Users/rajeshjain/projects/GreatLearnings/assignments/residency/gurgaonbatch-rajeshcjain/CapstonProject --exp_name=pretrained_model --max_enc_steps=400 --max_dec_steps=120 --coverage=1 --single_pass=1

You need to modify the path according to you folder structure.

Run it and you will get the output in the pretrained_model folder.

Now Lets see how can we install the pyrouge and get the result


----------------------------
To get the evaluation done
----------------------------

pip uninstall pyrouge
git clone https://github.com/bheinzerling/pyrouge
cd pyrouge
pip install -e .
pyrouge_set_rouge_path </absolute/path/to/ROUGE-1.5.5/directory>
python -m pyrouge.test


----------------
create eval.py
----------------

from pyrouge import Rouge155
r = Rouge155()
# set directories
r.system_dir = "/Users/rajeshjain/projects/GreatLearnings/assignments/residency/gurgaonbatch-rajeshcjain/CapstonProject/pretrained_model/decode_val_400maxenc_4beam_35mindec_120maxdec_ckpt-238410/decoded/"
r.model_dir = "/Users/rajeshjain/projects/GreatLearnings/assignments/residency/gurgaonbatch-rajeshcjain/CapstonProject/pretrained_model/decode_val_400maxenc_4beam_35mindec_120maxdec_ckpt-238410/reference/"

# define the patterns
r.system_filename_pattern = "(\d+)_decoded.txt"
r.model_filename_pattern = "#ID#_reference.txt"

# use default parameters to run the evaluation
output = r.convert_and_evaluate()
print(output)
output_dict = r.output_to_dict(output)

-------------------------------

python -m eval


Please remember we need to copy the rouge-1.5.5 and keep it in pyrouge folder.

If you don’t have then download the pyrouge from https://github.com/andersjo/pyrouge and copy ROUGE-1.5.5 from tools folder and past it in the above pyrouge don’t use this downloaded pyrouge..I faced lot of problem with it.

I could not spare time for docker file..I will start working on it as soon as I get time.
