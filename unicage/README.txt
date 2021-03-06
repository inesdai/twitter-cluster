Note:
  This analysys process is separated to 7 steps.
  "twitter_analysis.sh" is ignition point of all or each step.

  Usage)
    $ twitter_analysis.sh <start_step_no> <end_step_no>

    step_no:
      1 - list_word_pairings.sh
      2 - wgted_edge_gen.sh
      3 - unwgted_edge_gen.sh
      4 - run_mcliques.sh
      5 - run_cos.sh
      6 - back_to_org_words.sh
      7 - compute_transition_likelihoods.sh

   Example)
      To execute step4 to step6:
        $ twitter_analysis.sh 4 6
      To execute step2 only:
        $ twitter_analysis.sh 2 2
      To execute all steps:
        $ twitter_analysis.sh 1 7

   Notice)
      step1 and step7 will take much time (about 6 - 8 hours). 


More datail informations of each step as below.

  step1: list_word_pairings.sh
    creates lists of hashtag pairs from json files.
    produces DATA/result.XXXX.
  
  step2: wgted_edge_gen.sh
    creates weighted edgelists from result.* and place them under yyyymmdd dirs. 
    produces twitter/yyyymmdd/weighted_edges_yyyymmdd.txt
  
  step3: unwgted_edge_gen.sh
    creates unweighted edgelists under the same dir sorted by threshold dirs.
    produces twitter/yyyymmdd/th_XX/unweighted_yyyymmdd_th_XX.txt
  
  step4: run_mcliques.sh
    executes maximal_cliques to all unweigthed edges.
    produces twitter/yyyymmdd/th_XX/unweighted_edges_yyyymmdd_th_XX.txt.map and 
             twitter/yyyymmdd/th_XX/unweighted_edges_yyyymmdd_th_XX.txt.mcliques
  
  step5: run_cos.sh
    executes cos using *.mcliques files to create communities.
    produces twitter/yyyymmdd/th_XX/N_communities.txt
  
  step6: back_to_org_words.sh
    reverts integers in N_commnities.txt to original words using map file generated by maximal_cliques.
    produces twitter/yyyymmdd/th_XX/namedN_communities.txt
  
  step7: compute_transition_likelihoods.sh
    compute transition-likelihoods map files using named_N_communities.txt.
    produces twitter/yyyymmdd/th_XX/namedN_communities_transition.csv
  
