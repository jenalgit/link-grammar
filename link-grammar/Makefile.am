#
# Automake file for building liblink-grammar.so
#

SUBDIRS=

if LIBMINISAT_BUNDLED
MINISAT_DIR = minisat
endif

if WITH_SAT_SOLVER
SUBDIRS += $(MINISAT_DIR) sat-solver
endif

if WITH_CORPUS
SUBDIRS += corpus
endif

if OS_WIN32

install-libtool-import-lib:
	$(INSTALL) .libs/liblink-grammar.dll.a $(DESTDIR)$(libdir)

uninstall-libtool-import-lib:
	-rm $(DESTDIR)$(libdir)/liblink-grammar.dll.a
else
install-libtool-import-lib:
uninstall-libtool-import-lib:
endif

DEFS = @DEFS@ -DVERSION=\"@VERSION@\" -DDICTIONARY_DIR=\"$(pkgdatadir)\"

# $(top_builddir) to pick up autogened link-grammar/link-features.h
AM_CPPFLAGS = -I$(top_srcdir) -I$(top_builddir) $(WARN_CFLAGS) \
	$(HUNSPELL_CFLAGS)

lib_LTLIBRARIES = liblink-grammar.la

EXTRA_liblink_grammar_la_DEPENDENCIES = $(srcdir)/link-grammar.def

liblink_grammar_la_LDFLAGS = -version-info @VERSION_INFO@ \
	-export-dynamic -no-undefined \
	-export-symbols $(srcdir)/link-grammar.def \
	$(LINK_CFLAGS)

if OS_WIN32
liblink_grammar_la_LDFLAGS += -D_JNI_IMPLEMENTATION_ -Wl,--kill-at
endif

liblink_grammar_la_LIBADD  =  ${REGEX_LIBS}

if HAVE_HUNSPELL
liblink_grammar_la_LIBADD  +=  ${HUNSPELL_LIBS}
endif

if HAVE_ASPELL
liblink_grammar_la_LIBADD  +=  ${ASPELL_LIBS}
endif

if HAVE_SQLITE
liblink_grammar_la_LIBADD  +=  ${SQLITE3_LIBS}
endif

if WITH_SAT_SOLVER
liblink_grammar_la_LIBADD  += $(top_builddir)/link-grammar/sat-solver/libsat-solver.la
if LIBMINISAT_BUNDLED
liblink_grammar_la_LIBADD  += $(top_builddir)/link-grammar/minisat/libminisat.la
else !LIBMINISAT_BUNDLED
liblink_grammar_la_LIBADD  += ${MINISAT_LIBS}
endif !LIBMINISAT_BUNDLED
endif WITH_SAT_SOLVER

if WITH_CORPUS
liblink_grammar_la_LIBADD  += $(top_builddir)/link-grammar/corpus/liblink-corpus.la ${SQLITE3_LIBS}
endif

# Math libraries are needed for floorf, etc.
liblink_grammar_la_LIBADD  += -lm

liblink_grammar_la_SOURCES =        \
	analyze-linkage.c                \
	anysplit.c                       \
	api.c                            \
	build-disjuncts.c                \
	constituents.c                   \
	count.c                          \
	dict-common.c                    \
	dict-file/dictionary.c           \
	dict-file/read-dict.c            \
	dict-file/read-regex.c           \
	dict-file/word-file.c            \
	dict-sql/read-sql.c              \
	disjunct-utils.c                 \
	disjuncts.c                      \
	error.c                          \
	expand.c                         \
	extract-links.c                  \
	fast-match.c                     \
	histogram.c                      \
	idiom.c                          \
	linkage.c                        \
	post-process.c                   \
	pp_knowledge.c                   \
	pp_lexer.c                       \
	pp_linkset.c                     \
	preparation.c                    \
	print.c                          \
	print-util.c                     \
	prune.c                          \
	regex-morph.c                    \
	regex-tokenizer.c                \
	resources.c                      \
	score.c                          \
	spellcheck-aspell.c              \
	spellcheck-hun.c                 \
	string-set.c                     \
	tokenize.c                       \
	utilities.c                      \
	wcwidth.c                        \
	wordgraph.c                      \
	word-utils.c                     \
	anysplit.h                       \
	api-structures.h                 \
	api-types.h                      \
	analyze-linkage.h                \
	build-disjuncts.h                \
	count.h                          \
	dict-file/read-dict.h            \
	dict-file/read-regex.h           \
	dict-file/word-file.h            \
	dict-sql/read-sql.h              \
	dict-api.h                       \
	dict-common.h                    \
	dict-structures.h                \
	disjunct-utils.h                 \
	disjuncts.h                      \
	error.h                          \
	expand.h                         \
	externs.h                        \
	extract-links.h                  \
	fast-match.h                     \
	histogram.h                      \
	idiom.h                          \
	lg_assert.h                      \
	link-includes.h                  \
	linkage.h                        \
	post-process.h                   \
	pp_knowledge.h                   \
	pp_lexer.h                       \
	pp_linkset.h                     \
	preparation.h                    \
	print.h                          \
	print-util.h                     \
	prune.h                          \
	regex-morph.h                    \
	regex-tokenizer.h                \
	resources.h                      \
	score.h                          \
	spellcheck.h                     \
	string-set.h                     \
	structures.h                     \
	tokenize.h                       \
	utilities.h                      \
	wcwidth.h                        \
	wordgraph.h                      \
	word-utils.h

liblink_grammar_includedir = $(includedir)/link-grammar
liblink_grammar_include_HEADERS =   \
	link-features.h                  \
	link-includes.h                  \
	dict-api.h                       \
	dict-structures.h

EXTRA_DIST=                         \
	link-grammar.def                 \
	README.md                        \
	dict-sql/dict.sql                \
	dict-sql/demo.sql                \
	dict-sql/README

# -----------------------------------------------------------
install-data-local: install-libtool-import-lib

uninstall-local: uninstall-libtool-import-lib
