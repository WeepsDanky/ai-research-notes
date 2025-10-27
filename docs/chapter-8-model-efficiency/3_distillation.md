# Distillation

Train smaller model by learning from larger models. Knowledge can be transferred by different form of learning: 

* response distillation: concern only outputs of teacher model and student model try to exactly or similarly perform as teacher  
* feature distillation: uses last layer and intermediate layers to create better inner representations of student model
* and API distillation: use api from provider to train smaller model