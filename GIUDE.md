# Useful Commands

``` shell
 python generate.py   --load_8bit=True --langchain_mode=UserData --user_path=user_path share=True  

```

``` shell
 python generate.py   --load_8bit=True --langchain_mode=UserData --user_path=user_path share=True --trust-remote-code    
```



### Multiple embeddings and sources

We only support one embedding at a time for each database.

So you could use src/make_db.py to make the db for different embeddings (`--hf_embedding_model` like gen.py, any HF model) for each collection (e.g. UserData, UserData2) for each source folders (e.g. user_path, user_path2), and then at generate.py time you can specify those different collection names in `--langchain_modes` and `--langchain_modes` and `--langchain_mode_paths`.  For example:
```bash
python src/make_db.py --user_path=user_path --collection_name=UserData --hf_embedding_model=hkunlp/instructor-large
python src/make_db.py --user_path=user_path2 --collection_name=UserData2 --hf_embedding_model=sentence-transformers/all-MiniLM-L6-v2
```
then
```bash
python generate.py --base_model='llama' --prompt_type=llama2 --score_model=None --langchain_mode='UserData' --langchain_modes=['UserData','UserData2'] --langchain_modes=['UserData','UserData2'] --langchain_mode_paths={'UserData':'user_path','UserData2':'user_path2'}
```
and watch-out for use of whitespace.  For `langchain_mode_paths` you can pass surrounded by "'s and have spaces.
