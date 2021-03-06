## Nuclear Half-lives Chart
  <script src="https://root.cern/js/latest/scripts/JSRoot.core.js" type="text/javascript"></script>
  <div id="drawth2" style="width:600px; height:400px"></div>
  <div id="data source">
   <i>Data source : <a href="htts://www.nndc.bnl.gov/ensdf" target="_blank">Evaluated Nuclear Structure Data File</a>, last updated 2020-10-01 </i>
   </div>
  <div id="user_tooltip">Move cursor to display half-life value</div>
  <script type='text/javascript'>
     function UserHandler(info) {
        if (!info)  {
           d3.select("#user_tooltip").html("No tooltip");
           return false;
        }
        var ele = ["H", "He", "Li", "Be", "B", "C", "N", "O", "F", "Ne", "Na", "Mg", "Al", "Si", "P", "S", "Cl", "Ar", "K", "Ca", "Sc", "Ti", "V", "Cr", "Mn", "Fe", "Co", "Ni", "Cu", "Zn", "Ga", "Ge", "As",
						"Se", "Br", "Kr", "Rb", "Sr", "Y", "Zr", "Nb", "Mo", "Tc", "Ru", "Rh", "Pd", "Ag", "Cd", "In", "Sn", "Sb", "Te", "I", "Xe", "Cs", "Ba", "La", "Ce", "Pr", "Nd", "Pm", "Sm", "Eu", "Gd", "Tb", "Dy",
						"Ho", "Er", "Tm", "Yb", "Lu", "Hf", "Ta", "W", "Re", "Os", "Ir", "Pt", "Au", "Hg", "Tl", "Pb", "Bi", "Po", "At", "Rn", "Fr", "Ra", "Ac", "Th", "Pa", "U", "Np", "Pu", "Am", "Cm", "Bk", "Cf", "Es",
						"Fm", "Md", "No", "Lr", "Rf", "Db", "Sg", "Bh", "Hs", "Mt", "Ds", "Rg", "Cn", "Nh", "Fl", "Mc", "Lv", "Ts", "Og"];
					
        // set tooltip info
        var A = info.binx+info.biny-2;
        var Z = info.biny-1;
        var element = ele[Z-1];
        d3.select("#user_tooltip").html("Isotope: <sup>"+ A +"</sup>"+ element +" | T<sub>1/2</sub> = " + info.cont.toFixed(4)+" s");
        return true; // means event is handled and can be ignored
     }
     JSROOT.openFile("https://ribf.riken.jp/~phong/halflives.root").then(file => {
        file.readObject("halflives;1")
            .then(obj2 => JSROOT.draw("drawth2", obj2, "colz;logz;nostat").then(painter =>{
              painter.configureUserTooltipHandler(1 ? UserHandler : null);
            }));
     });
   </script>
