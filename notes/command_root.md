---
layout: page
title: "ROOT"
permalink: /root/
---

# Commands for ROOT
### Browse the root file
Use a [TBrowser](https://root.cern.ch/doc/master/classTTreeViewer.html)

```
root [0] gSystem->Load("TTreeViewer");
root [1] TFile file("<file_name>.root");
root [2] new TTreeViewer("<tree_name>");
```
Or can do this: `TBrowser b("<file_name.root>");`

the class of an object is the text before the first underline, "\_" . 
In general, the object can be grabbed via `*<gallery::Event>.getValidHandle()` function.


open a root file:

    root -l <name>.root

show classes in the root file:

    .ls

Show detail variables of an object (the $n$th object in an example):

    vertex_tree->Show(n)

Show brief summary:

    vertex_tree->Scan()

Save this summary to a file:

	((TTreePlayer*)(T->GetPlayer()))->SetScanRedirect(true); 
	((TTreePlayer*)(T->GetPlayer()))->SetScanFileName("toto.txt"); 
   	tree->Scan(...);  

Show number of Entries:

    vertex_tree->GetEntries()

Plot according to a given variable

    vertex_tree->Draw("<object>","<condition 1>&&<condition 2>")

Plot according to a given variable (with customized bins, e.g. 30 bins ranged from 0 to 1)

    vertex_tree->Draw("<object>>>hsqrt(30,0,1)","<condition 1>&&<condition 2>")


---
Make a canvas for multiple plots (e.g. a 2 columns by 2 rows canvas):

    TCanvas * c = new TCanvas();
    c->Divide(2,2);
then change to one of the canvas:

    c->cd(1)

---
Insert a line in to a histogram (???):

    ?????.Fit("pol n")

---
Connect a friend tree (add tree in file2.root to the file1.root)T

    TFile f1("file1.root"); //open a root file
    TTree * Tree_name = (TTree* )f1.Get("<Existant_Tree_name>");//make a new tree (e.g. vertex_tree) in the root file f1
    Tree_name->AddFriend("Friend_tree = Tree_name","file2.root")//copy (link) a friend a tree (e.g. lee_unfolding_tree) to the current root file.
    TF->Draw("things to draw");

*correction*

    Tree_name->AddFriend("Tree_name = Friend_tree","file2.root")//copy (link) a friend a tree (e.g. lee_unfolding_tree) to the current root file.
---
UI browser

    Tbrowser b

---
Draw 2D Histogram (y-axis:x-axisTl)

    vertex_tree->Draw("(reco_shower_helper_energy+reco_track_energy_new_legacy):(nu_energy)>>h(100,0,1.5,100,0,1.5)","abs(true_nuvertz-true_track_startz)<1","COLZ")

---
Weight a event, multiple it by some number:

    vertex_tree->Draw("nu_energy","lee_unfolding_tree.signal_weight","hist")

---
Set axis of a plot

    h->GetXaxis()->SetTitle("name of the x-axis")

Update the canvas

    c1->Update()

###Drawing
Binning (20 bins, from 0 to 0.7):

    vertex_tree->Draw("nu_energy>>Vertice(20,0,0.7)","signal_weight","hist")

Set title:

    Vertice->SetTitle("Unfolded Intrinsic #nu_{e}(#bar{#nu}_{e}) Flux Low Energy Excess")
    Vertice->GetXaxis()->SetTitle("MC True (Anti-)Electron Neutrino Energy")
    Vertice->GetYaxis()->SetTitle("Number of vertices")
    c1->Update()

#### Draw with special variables
[Special function](https://root.cern.ch/doc/master/classTTree.html)
	
`Sum$(variable)` will get the sum of each elements in that variable;


###Summary of result via TMVAGui
Run a root file:

    TMVA::TMVAGui("cosmic_template_training.root")

### Make a TTree Class
`<TTree_name>->MakeClass("output_file_name")`

### Delete a TDirecory

Go to update, mode, delete TDirectoryFile contain name `MCUnisim`, which has two cycle (contains objects inside, no subdirectory inside).
```
TFile f("hist_elEnuQE_bgap25_s1_h8261672200918285872.root ","update")
f.Delete("*MCUnisims*;2")
f.Write()
```

### Disable warnings
```
gSystem->RedirectOutput("/dev/null");
 gSystem->RedirectOutput(0,0);//re-activate the pirnt out.
```

### Math

#### TDecompLU
`TDecompLU lu(A)` decomposes a matrix `A` into $$PA=LU$$, where $P$ is a permutation matrix, $L$ is unit lower triangular, $U$ is upper triangular. That is, $A$ is analyzed, and $P$, $L$, $U$ are available for further use.

`lu.Decompose()` 

#### TMatrix
Get dimensions `<TMatrix>->GetNrows()`

Get contents, (1,1) for example, `(*<TMatrix>)(1,1)`


### Bug from the script

#### Drawing issue

```
T->Draw("var1","var2")

Warning in <TCanvas::ResizePad>: Inf/NaN propagated to the pad. Check drawn objects.
```

This could be caused by the Float_t numbers in `var2` with infinite digits, and it can be "fixed" by limiting the digits of `var2` (change it into int and change it back to Float_t).


