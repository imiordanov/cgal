project( BGL_surface_mesh_Examples )

cmake_minimum_required( VERSION 2.8.10 )

find_package( CGAL QUIET )

if ( NOT CGAL_FOUND )
  message( STATUS "This project requires the CGAL library, and will not be compiled." )
  return()
endif()

include( ${CGAL_USE_FILE} )

# include for local package
include_directories( BEFORE "../../include" )

include( CGAL_CreateSingleSourceCGALProgram )

create_single_source_cgal_program( "prim.cpp" )
create_single_source_cgal_program( "gwdwg.cpp" )
create_single_source_cgal_program( "seam_mesh.cpp" )
create_single_source_cgal_program( "write_inp.cpp" )
create_single_source_cgal_program( "surface_mesh_dual.cpp" )
create_single_source_cgal_program( "connected_components.cpp" )

find_package( METIS )

if( METIS_FOUND )
  include_directories(${METIS_INCLUDE_DIRS} )

  create_single_source_cgal_program( "surface_mesh_partition.cpp" )
  target_link_libraries( surface_mesh_partition PRIVATE ${METIS_LIBRARIES} )
else()
  message( STATUS "Examples that use the METIS library will not be compiled." )
endif()

