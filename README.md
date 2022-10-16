Global AI Hub Derin Öğrenme Bootcamp Final Projesi


Dataset: https://urbansounddataset.weebly.com/

Librosa: https://librosa.org/doc/latest/index.html

OpenCV :  https://docs.opencv.org/4.x/d9/df8/tutorial_root.html
- Bu projede UrbanSounds8K veri seti kullanılarak şehirde duyulan seslerin sınıflandırılması gerçekleştirildi. 

## Spectrogramların oluşturulması: 
- Ses dosyalarından oluşan datasette bulunan 8732 veri incelendi. Spectrogramları oluştururken Librosa kullanıldı. 
- Librosa müzik ve ses analizi için kullanılan bir Python paketidir.
- Ses dosyalarının spectrogramları "librosa.feature.melspectrogram()" kullanılarak oluşturuldu. 

 ![spect](https://user-images.githubusercontent.com/41507884/195982427-c5560195-d0a8-42ed-9f14-0a8827b4fd7a.png)


## Preproccesing:
- Spectrogram verileri tek tek okunarak grayscale dönüşüm, resizing, normalizasyon işlemleri gerçekleştirildi. 
- Bu işlemler gerçekleştirilirken bir görüntü işleme kütüphanesi olan OpenCV kullanıldı.
- İşlemler gerçekleştirildikten sonra veriler etiketleriyle birlikte bir listeye eklendi.

- Bu liste kullanılarak train\test\val veri setleri hazırlandı. Bir bölümü üzerinde model çalışılması (train) diğer bölüm üzerinde model iyileştirilmesi (validation) ve başka bir bölümde de test edilmesi amacıyla modelleme yapmadan önce verilerin 3 ayrı parçaya ayrılması gerekiyor.
- Veri setlerinin ayrıştırılması için "sklearn" kütüphanesinden yararlanıldı.

## Model:
- CNN modeli oluşturmak için "TensorFlow" kütüphanesi kullanıldı. 
- İlk modelde activasyon fonk. "ReLU", "Softmax"; optimizer "Adam" ve loss fonk. "sparse_categorical_crossentropy"; Batch size "64", epoch "20" olarak belirlendi.

![model1acc](https://user-images.githubusercontent.com/41507884/195982656-e50002f4-e393-4998-937f-4b4128f679c6.png)![model1loss](https://user-images.githubusercontent.com/41507884/195982668-735ef8e2-30bd-47fc-a39d-307f08a6dadd.png)

- Performans metrikleri: Accuracy: 0.8305 loss: 0.6600 olarak hesaplandı. 
- Hiperparametre optimizasyonu için yeni bir model oluşturuldu. 

- İkinci modelde activasyon fonk. "ReLU", "Softmax"; optimizer "RMSProp"; loss fonk. "sparse_categorical_crossentropy"; Batch size "128", epoch "30" olarak belirlendi.
- İlk modelden farklı olarak katman eklemesi yapıldı. (Conv2D, BatchNormalization)

![model2acc](https://user-images.githubusercontent.com/41507884/195982895-bdd407b1-e5a4-4024-ab11-77bb4dd9e9bf.png)![model2loss](https://user-images.githubusercontent.com/41507884/195982894-42d21c7a-8c3c-4ed6-b010-609d002296ff.png)

- Performans metrikleri: Accuracy: 0.9255 loss: 0.3379  olarak hesaplandı. 


