# [ACL 2024] VisDiaHalBench: A Visual Dialogue Benchmark For Diagnosing Hallucination in Large vision-Language Models

## Download link

The full dataset can be downloaded [here](https://)

## Data format
This repo contains examples of the dataset, which has the following format:

    .
    ├── images                   
    │   ├── 70                                     # image folder named with its image-id in GQA dataset.
    │   │   ├── org.png                            # The original image in the GQA dataset.
    │   │   ├── change_attr|modif_obj|remove.png   # The edited image depends on its edit type.
    │   │   ├── info.txt                           # The image edition information
    │   ├── (image id) 
    ├── QA_info.json                               # The dialogue question-answer annotation.
    └── README.md

"QA_info.json" contains 5000 dialogue annotations. It is a dict where the key is the image id, the value is its annotation:

```
{ 
 (image id):
    { dialogue: list, 
    edit_information: dict },
 ...  
}
```

"dialogue" is a list that contains five-turn question-answer pairs and related information:

```
{
 "question"                       # The natural language question.
 "answer"                         # The groundtruth answer
 "question_type"                  # The type of the question: “exist”, “queryObject”, “queryAttr”, “queryRel”, “verifyAttr”, “verifyRel”, “verifyTargetAttr”, “verifyTargetRel”.
 "answer_type":                   # The type of the answer: "YN", "obj", "attr", "rel"
 "object_chain"                   # A list of scene graph triplets path used to generate the question.
 "answer_triplets"                # The triplets related to the groundtruth answer.
 "image_id"                       # The id of the corresponding image in the GQA dataset.
 "round"                          # The dialogue round of this QA.
 "hallucination_type"             # The hallucination type of this QA.
 "last_round_input"               # The object/attribute/relation that this QA refers to
}
```

"edit_information" is a dict that describes how the image is edited:

```
{
 "edit_type"                      # The edit type of this sample: change_attr, modif_obj, remove
 "edited_sg"                      # The corresponding scene graph after editing the image. It has the same format as GQA.
 "edited_object_id"               # The id of the object in this scene graph.
 "edit_params"                    # The edition information, describing how to modify the object.
}
```

## Results and code

The dataset differs slightly from the ACL paper, where we use a more proper prompt to generate questions with GPT-4 and do not change some background objects. We are rerunning the experiments and will release the results and code soon.
