CFLAGS= -fprofile-arcs -ftest-coverage -fPIC

all: links
	$(CXX) $(CFLAGS) -c subdir/A/file1.cpp -o subdir/A/file1.o
	$(CXX) $(CFLAGS) -c subdir/A/file2.cpp -o subdir/A/file2.o
	$(CXX) $(CFLAGS) -c subdir/A/file3.cpp -o subdir/A/file3.o
	$(CXX) $(CFLAGS) -c subdir/A/file4.cpp -o subdir/A/file4.o
	$(CXX) $(CFLAGS) -c subdir/A/file7.cpp -o subdir/A/file7.o
	$(CXX) $(CFLAGS) -c subdir/A/C/file5.cpp -o subdir/A/C/file5.o
	$(CXX) $(CFLAGS) -c subdir/m/n/C/D/file6.cpp -o subdir/m/n/C/D/file6.o
	$(CXX) $(CFLAGS) -c subdir/B/main.cpp -o subdir/B/main.o
	$(CXX) $(CFLAGS) subdir/A/file1.o subdir/A/file2.o subdir/A/file3.o subdir/A/file4.o subdir/A/C/file5.o subdir/m/n/C/D/file6.o subdir/A/file7.o subdir/B/main.o -o subdir/testcase

run: txt xml html sonarqube json

txt:
	./subdir/testcase
	$(GCOVR) -d -o coverage.txt

xml:
	./subdir/testcase
	$(GCOVR) -d -x -o coverage.xml

html:
	./subdir/testcase
	$(GCOVR) -d --html-details -o coverage.html

sonarqube:
	./subdir/testcase
	$(GCOVR) -d --sonarqube sonarqube.xml

json:
	# pass

clean:
	rm -Rf subdir
	rm -f coverage.txt coverage.xml coverage*.html sonarqube.xml

links:
	if ! [ -d "subdir" ]; then\
	   mkdir subdir;\
	   cd subdir;\
	   ln -s ../../nested/subdir/B .;\
	   mkdir -p m;\
	   cd m;\
	   ln -s ../../../nested/subdir/A n;\
	   cd ..;\
	   ln -s m/n A;\
	   ln -s . loop;\
	   cd ..;\
	fi
