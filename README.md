# MD-GNN

A pre-process method of graph against adversarial attacks

# Requirement

- matplotlib == 3.2.2

- torch_geometric == 1.5.0
- networkx == 2.4
- tqdm == 4.46.1
- torch == 1.5.0
- seaborn == 0.10.1
- scipy == 1.4.1
- numpy == 1.18.1
- openpyxl == 3.0.6
- deeprobust == 0.2.1
- scikit_learn==0.24.2

# Run Test

- run test

  ```shell
  python test.py
  ```

- run MD-GCN

  ```python
  # datasets：['cora', 'citeseer', 'cora_ml']
  # attack：['meta', 'nettack', 'random']
  # metric：['Cfs', 'Cfs1', 'Cfs2', 'Cfs3', 'Cfs4', 'Cs', 'Cs1', 'Jaccard1']
  device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
  
  data = Dataset(root='data/', name='cora', seed=15, require_mask=True)
  data.adj = sp.load_npz('adv_adj/cora_meta_adj_0.25.npz')
  output, time = CFS1(data, device, 'Cfs')
  ```

- run experiments

  ```python
  from src.generate_experiment_data import *
  from src.generate_experiment_figure import *
  from src.save_excel import *
  
  dataset_list = ['cora', 'citeseer', 'cora_ml']
  attack_list = ['meta', 'nettack', 'random']
  defense_list = ['GCN', 'GCNSVD', 'Jaccard', 'ProGNN', 'RGCN', 'GAT', 'CFS', 'CfsGAT', 'CfsRGCN', 'GNNGuard', 'HGCN', 'CfsHGCN']
  root = 'data/'
  root1 = 'adv_adj/'
  save_dir = 'experiment/data/0/'
  
  threshold_list = [0.03, 0.05]
  a = [0.05, 0.1]
  lr_list = [0.001, 0.005, 0.01, 0.05, 0.1]
  
  # Experiments 1 ~ 5
  experiment1(dataset_list, attack_list,defense_list, root, root1, save_dir)
  experiment2(dataset_list, attack_list, threshold_list, root, root1, save_dir)
  experiment3(dataset_list, attack_list, root, root1, save_dir, a)
  experiment4(dataset_list, attack_list, defense_list, root, root1, save_dir, 'Cfs4')
  experiment5(dataset_list, attack_list, lr_list, root, root1, save_dir, 'Cfs', 10)
  
  # Experimental Figures 1 ~ 4
  figure1()
  figure2()
  figure3()
  figure4()
  
  # Experimental tables
  result()
  result_time()
  ```

- others

  ```python
  run generate_adv.py #生成对抗样本
  ```

  ```shell
  run generate_clean.py #生成MD预处理后的图邻接矩阵
  ```

  

# Project Structure

- MD-GNN
  - adv-adj：saved adversarial samples
  - data：original data
  - defense：defence approaches
  - experiment：saved data
  - src：drawing results
  - generate_adv.py
  - generate_clean.py
  - test.py
  - utils.py：self-defined utility function
