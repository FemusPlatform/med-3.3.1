include $(top_srcdir)/config/automake.common
include $(top_srcdir)/config/test.am

if WITH_PYTHON


#TESTS_ENVIRONMENT = eval python -c "__file__='.libs'" <
#TESTS_ENVIRONMENT = python -c '__file__=".libs" ' <

# TESTS_ENVIRONMENT = eval H5DUMP=@H5DUMP@ SRCDIR=$(srcdir) SRCDIR="$(abs_srcdir)" BUILDDIR="$(abs_builddir)" \
# 		EXECDIR="$(abs_builddir)" CP=${CP} CPYMED="no"
#TESTS_ENVIRONMENT += OUTPUT="yes" CHECKER="libtool\ --mode=execute\ valgrind\ --error-limit=no"

tests_params.py: $(srcdir)/Makefile.am 
	echo "USER_MODE=MED_COMPACT_STMODE" > $@.tmp ; \
	echo "USER_INTERLACE=MED_FULL_INTERLACE" >> $@.tmp ; \
	echo "MEDARRAY_TYPEF=MEDFLOAT" >> $@.tmp ; \
	echo "MEDARRAY_TYPEI=MEDINT" >> $@.tmp ; \
	echo "FIELD_TYPEF=MED_FLOAT64" >> $@.tmp ; \
	echo "FIELD_TYPEI=MED_INT" >> $@.tmp ; \
	echo "PARAM_ID=''" >> $@.tmp ; \
	mv $@.tmp $@

tests_params_f64_i32.py: $(srcdir)/Makefile.am 
	echo "USER_MODE=MED_COMPACT_STMODE" > $@.tmp ; \
	echo "USER_INTERLACE=MED_FULL_INTERLACE" >> $@.tmp ; \
	echo "MEDARRAY_TYPEF=MEDFLOAT64" >> $@.tmp ; \
	echo "MEDARRAY_TYPEI=MEDINT32" >> $@.tmp ; \
	echo "FIELD_TYPEF=MED_FLOAT64" >> $@.tmp ; \
	echo "FIELD_TYPEI=MED_INT32" >> $@.tmp ; \
	echo "PARAM_ID='_f64_i32'" >> $@.tmp ; \
	mv $@.tmp $@

tests_params_f64_i64.py: $(srcdir)/Makefile.am 
	echo "USER_MODE=MED_COMPACT_STMODE" > $@.tmp ; \
	echo "USER_INTERLACE=MED_FULL_INTERLACE" >> $@.tmp ; \
	echo "MEDARRAY_TYPEF=MEDFLOAT64" >> $@.tmp ; \
	echo "MEDARRAY_TYPEI=MEDINT64" >> $@.tmp ; \
	echo "FIELD_TYPEF=MED_FLOAT64" >> $@.tmp ; \
	echo "FIELD_TYPEI=MED_INT64" >> $@.tmp ; \
	echo "PARAM_ID='_f64_i64'" >> $@.tmp ; \
	mv $@.tmp $@

tests_params_f32_i32.py: $(srcdir)/Makefile.am
	echo "USER_MODE=MED_COMPACT_STMODE" > $@.tmp ; \
	echo "USER_INTERLACE=MED_FULL_INTERLACE" >> $@.tmp ; \
	echo "MEDARRAY_TYPEF=MEDFLOAT32" >> $@.tmp ; \
	echo "FIELD_TYPEF=MED_FLOAT32" >> $@.tmp ; \
	echo "MEDARRAY_TYPEI=MEDINT32" >> $@.tmp ; \
	echo "FIELD_TYPEI=MED_INT32" >> $@.tmp ; \
	echo "PARAM_ID='_f32_i32'" >> $@.tmp ; \
	mv $@.tmp $@

tests_params_f32_i64.py: $(srcdir)/Makefile.am
	echo "USER_MODE=MED_COMPACT_STMODE" > $@.tmp ; \
	echo "USER_INTERLACE=MED_FULL_INTERLACE" >> $@.tmp ; \
	echo "MEDARRAY_TYPEF=MEDFLOAT32" >> $@.tmp ; \
	echo "FIELD_TYPEF=MED_FLOAT32" >> $@.tmp ; \
	echo "MEDARRAY_TYPEI=MEDINT64" >> $@.tmp ; \
	echo "FIELD_TYPEI=MED_INT64" >> $@.tmp ; \
	echo "PARAM_ID='_f32_i64'" >> $@.tmp ; \
	mv $@.tmp $@


#Créer les fichiers de paramètres par test à partir des fichiers de référence précédents
SUFFIXES+= _params_f64_i32.py _params_f32_i32.py _params_f64_i64.py _params_f32_i64.py

#Parceque les dépendances des règles double-suffixe n'utilisent pas les prérequis
#à l'application des règles
test10_params_f64_i32.py : tests_params_f64_i32.py
test10_params_f32_i32.py : tests_params_f32_i32.py
test10_params_f64_i64.py : tests_params_f64_i64.py

.py_params_f64_i32.py:
	${CP} -f tests_params_f64_i32.py $@
.py_params_f32_i32.py:
	${CP} -f tests_params_f32_i32.py $@
.py_params_f64_i64.py:
	${CP} -f tests_params_f64_i64.py $@
.py_params_f32_i64.py:
	${CP} -f tests_params_f32_i64.py $@

test10_params_f32_i64.py : tests_params_f32_i64.py

TESTS_PARAMS= tests_params.py \
tests_params_f64_i32.py tests_params_f32_i32.py \
tests_params_f64_i64.py tests_params_f32_i64.py \
test10_params_f64_i32.py test10_params_f32_i32.py \
test10_params_f64_i64.py test10_params_f32_i64.py

#Création des différents executables (ex: test10_f64_i32.py)
SUFFIXES+= _f64_i32.py _f32_i32.py _f64_i64.py _f32_i64.py

.py_f64_i32.py :
	${SED} 's/_TEST_PARAMS_PY_/_params_f64_i32.py/g' $< > $@
.py_f32_i32.py :
	${SED} 's/_TEST_PARAMS_PY_/_params_f32_i32.py/g' $< > $@
.py_f64_i64.py :
	${SED} 's/_TEST_PARAMS_PY_/_params_f64_i64.py/g' $< > $@
.py_f32_i64.py :
	${SED} 's/_TEST_PARAMS_PY_/_params_f32_i64.py/g' $< > $@


BUILT_SOURCES= ${TESTS_PARAMS} \
test10_f64_i32.py test10_f32_i64.py test10_f64_i64.py test10_f32_i64.py

#test11_f64.py test11_f32.py
# test10_f32_i32.py test10_f32_i64.py test10_i32.py test10_i64.py


# check-local: 


testpydir = $(bindir)/testpy

INSTALLCHECK_TESTS_ENVIRONMENT = AUTOTEST_PATH=$(testpydir) PYTHONPATH=$(pyexecdir) H5DUMP=@H5DUMP@ SRCDIR=$(srcdir) ABSSRCDIR="$(abs_srcdir)" BUILDDIR=$(abs_builddir) EXECDIR="$(abs_builddir)" CP=${CP} CPYMED="no" MEDINT="_@LONG_OR_INT@"

# TESTS = test1.sh $(TESTS_ECR) $(TESTS_LEC)

TESTS_LEC = test3.py test5.py test7.py test9.py \
            test11.py test13.py test22.py test24.py test28.py test30.py 
#test3.py test15.py test17.py test26.py test32.py test33.py

TESTS_ECR = test1.py test2.py test4.py test6.py test8.py \
	test10_f64_i32.py test10_f32_i32.py  \
	test10_f64_i64.py test10_f32_i64.py  \
	test12.py test21.py test23.py test27.py test29.py \
	test_medfile.py test_medmesh.py \
	UseCase_MEDinterp_1.py \
	UseCase_MEDinterp_2.py \
	UseCase_MEDinterp_3.py
#test2.py test14.py test16.py test20.py test18.py test25.py test31.py

# EXTRA_DIST = test1.py
EXTRA_DIST += BECAREFUL 
EXTRA_DIST += \
test11_f32_i32_int.expout\
test11_f32_i64_int.expout\
test11_f64_i32_int.expout\
test11_f64_i64_int.expout\
test11_f32_i32_long.expout\
test11_f32_i64_long.expout\
test11_f64_i32_long.expout\
test11_f64_i64_long.expout


CHECK_TESTS_LEC = $(srcdir)/test3.atpy $(srcdir)/test5.atpy $(srcdir)/test7.atpy $(srcdir)/test9.atpy \
            $(srcdir)/test11.atpy $(srcdir)/test13.atpy \
            $(srcdir)/test22.atpy $(srcdir)/test24.atpy $(srcdir)/test28.atpy \
	    $(srcdir)/test30.atpy 
#$(srcdir)/test3.atpy $(srcdir)/test15.atpy $(srcdir)/test17.atpy $(srcdir)/test26.atpy $(srcdir)/test32.atpy $(srcdir)/test33.atpy

CHECK_TESTS_ECR = $(srcdir)/test1.atpy $(srcdir)/test2.atpy $(srcdir)/test4.atpy $(srcdir)/test6.atpy $(srcdir)/test8.atpy \
	$(srcdir)/test10.atpy $(srcdir)/test12.atpy \
	$(srcdir)/test21.atpy  $(srcdir)/test23.atpy \
	$(srcdir)/test27.atpy $(srcdir)/test29.atpy \
	$(srcdir)/test_medfile.atpy \
	$(srcdir)/test_medmesh.atpy \
	$(srcdir)/UseCase_MEDinterp_1.atpy \
	$(srcdir)/UseCase_MEDinterp_2.atpy \
	$(srcdir)/UseCase_MEDinterp_3.atpy

if INSTALLTEST
testpy_PYTHON= ${TESTS_PARAMS} $(TESTS_ECR) $(TESTS_LEC)
endif

PYTHONINSTALLCHECK_TESTS += $(CHECK_TESTS_LEC) $(CHECK_TESTS_ECR) 
# PYTHONINSTALLCHECK_PROGS += $(CHECK_TESTS_LEC) $(CHECK_TESTS_ECR)

endif

CLEANFILES+= UsesCase_MEDinterp_1.med \
./test1.med\
./test2.med\
./test4.med\
./test6.med\
./test8.med\
./test10.med\
./test10_f32.med\
./test10_f64.med\
./test12.med\
./test14.med\
./test16.med\
./test18.med\
./test20.med\
./test21.med\
./test23.med\
./test25.med\
./test27.med\
./test29.med\
./test31.med\
./test10.dump\
./test12.dump\
./test14.dump\
./test16.dump\
./test18.dump\
./test19.dump\
./test1.dump\
./test20.dump\
./test2.dump\
./test4.dump\
./test6.dump\
./test8.dump\
./test21.dump\
./test23.dump\
./test25.dump\
./test27.dump\
./test28.dump\
./test29.dump\
./test31.dump

CLEANFILES+=  ${BUILT_SOURCES} tests_params*.py.tmp

# SUBDIRS = dumps.ref .
SUBDIRS =  .

EXTRA_DIST += CMakeLists.txt

