set(comp_sources ImpedanceController.cpp ImpedanceControllerService_impl.cpp JointPathEx.cpp RatsMatrix.cpp ImpedanceOutputGenerator.h ../TorqueFilter/IIRFilter.cpp)
set(libs hrpModel-3.1 hrpCollision-3.1 hrpUtil-3.1 hrpsysBaseStub)
add_library(ImpedanceController SHARED ${comp_sources})
target_link_libraries(ImpedanceController ${libs})
set_target_properties(ImpedanceController PROPERTIES PREFIX "")

add_executable(ImpedanceControllerComp ImpedanceControllerComp.cpp ${comp_sources})
target_link_libraries(ImpedanceControllerComp ${libs})

add_executable(testImpedanceOutputGenerator testImpedanceOutputGenerator.cpp ImpedanceOutputGenerator.h RatsMatrix.cpp)
target_link_libraries(testImpedanceOutputGenerator ${libs})

add_library(JointPathExC SHARED JointPathExC.cpp JointPathEx.cpp)
target_link_libraries(JointPathExC ${libs})

set(target ImpedanceController ImpedanceControllerComp testImpedanceOutputGenerator JointPathExC)

add_test(testImpedanceOutputGeneratorTest0 testImpedanceOutputGenerator --test0 --use-gnuplot false)
add_test(testImpedanceOutputGeneratorTest1 testImpedanceOutputGenerator --test1 --use-gnuplot false)

install(TARGETS ${target}
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
)

