## 본 레포지토리는 네이버 부스트캠프 AI Tech 7기의 MRC 프로젝트에서의 RAG를 직접 구현한 뒤, 쉽게 사용할 수 있도록 가공한 Template입니다.

## 쓰는법
### 1. howtouse_MRC 를 본다. (대부분의 설명이 적혀 있습니다.)
### 2. arguments.py에서 바꿀 부분을 고른다. 

(Generation_based_MRC_arguments, 
Extraction_based_MRC_arguments,
Dense_search_retrieval_arguments, 
TF_IDF_retrieval_arguments를 ctrl + f를 통해 찾아서 고칩니다.)

### 3. 바꿀 부분을 바꾼다.

retrieval을 선언하고 build_faiss()
retrieval_model.search()를 하면 test데이터셋에 대한 retrieval 결과가 나옵니다.
이를 mrcmodel.inference(retrieval_result)에 넣으면 predict_result 폴더에 json 파일이 생성됩니다.

## 구성

본 템플릿에서는 BM25, Dense retrieval, TF-IDF 세 가지의 retrieval로 구성되어 있습니다.
Generator는 Extraction based Reader 와 Generation based Reader로 구성되어 있습니다.

### Retrieval
> 리트리버는 한 모델을 단독으로 사용할 수 있으여, model.search_query(mode = 'test')를 통해 추론할 수 있습니다.
model.search_query(mode = 'eval')을 통해 validation 결과를 acc로 확인해볼 수 있습니다.
또한, BM25 모델과 Dense passage retrieval을 같이 사용하여 Sequential Reranking 또는 Cross reranking을 통해 더 Robust하고 정확한 결과물을 얻을 수 있습니다.

### Reader
> Reader은 Extraction based reader과 generation based reader을 사용할 수 있습니다.
Extraction based reader은 주어진 context에서 max_length를 초과하는 text들을 다음의 입력으로 100자~200자 정도 겹치게 추가하여 모델이 긴 context에도 문맥을 읽을 수 있도록 학습합니다.
> Generation based reader는 기본적인 형태만 구현돼 있지만, 초과하는 context에 대한 대응을 할 수 있도록 구성돼 있지는 않습니다.


