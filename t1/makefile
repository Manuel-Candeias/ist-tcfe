hello: mesh nodal ngspice
	echo "Status norminal"

mesh:
	octave ./mat/meshm.m
	
nodal:
	octave ./mat/nodalm.m

ngspice: ngspice.log
	$(eval NGSTABS=$(shell grep _TAB $< | sed 's/_TAB//g' | sed ':a;N;$!ba;s/\n/ /g'))
	$(foreach i, $(NGSTABS), sed -n '/^$i_TAB/,/^$i_END/{p;/^$i_END/q}' $< | grep -v $i_TAB | grep -v $i_END | grep -v '#' | sed 's/\=/\&/g' | sed 's/$$/\\\\ \\hline/g' > $i_tab.tex;)
	



ngspice.log: ./sim/t1.cir
	ngspice -b $< -o $@

clean:
	rm -f nodal* mesh* ngspice.log ngspice op_tab.tex
	
