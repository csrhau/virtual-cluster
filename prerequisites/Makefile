.PHONY: all clean
.DEFAULT: all

define REQUIRE_IMPL
all: $1-$2.$3.$4.tar.gz
$1-$2.$3.$4.tar.gz: VERSION_MAJOR=$2
$1-$2.$3.$4.tar.gz: VERSION_MINOR=$3
$1-$2.$3.$4.tar.gz: VERSION_PATCH=$4
DOWNLOADS += $1-$2.$3.$4.tar.gz
endef

define REQUIRE_OMPI
$(call REQUIRE_IMPL,openmpi,$1,$2,$3)
endef

define REQUIRE_MPICH
$(call REQUIRE_IMPL,mpich,$1,$2,$3)
endef

define REQUIRE_GCC
$(call REQUIRE_IMPL,gcc,$1,$2,$3)
endef

# Download Prerequisites
$(eval $(call REQUIRE_GCC,7,2,0))
$(eval $(call REQUIRE_GCC,6,3,0))
$(eval $(call REQUIRE_GCC,5,4,0))
$(eval $(call REQUIRE_OMPI,3,0,1))
$(eval $(call REQUIRE_OMPI,1,10,2))
$(eval $(call REQUIRE_OMPI,1,8,8))
$(eval $(call REQUIRE_MPICH,3,2,1))

CURL= curl -sL

GCC_REMOTE = ftp://ftp.gnu.org/gnu/gcc/
OPENMPI_REMOTE = https://download.open-mpi.org/release/open-mpi
MPICH_REMOTE = http://www.mpich.org/static/downloads

gcc-%:
	$(CURL) -o $@ $(GCC_REMOTE)/gcc-$(VERSION_MAJOR).$(VERSION_MINOR).$(VERSION_PATCH)/$@

openmpi-%:
	$(CURL) -o $@ $(OPENMPI_REMOTE)/v$(VERSION_MAJOR).$(VERSION_MINOR)/$@

mpich-%:
	$(CURL) -o $@ $(MPICH_REMOTE)/$(VERSION_MAJOR).$(VERSION_MINOR).$(VERSION_PATCH)/$@

.PHONY: clean
clean:
	$(RM) $(DOWNLOADS)
