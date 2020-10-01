# blockchain-demo
Basicly demo how blockchain work
import React from 'react';
import { Route } from 'react-router-dom';
import PropTypes from 'prop-types';
import { connect } from 'react-redux';
import S2BMenu from '../../components/subComponents/S2BMenu';
import LoginPage from '../login';
import DirectDebitPage from './directdebit';
import DirectDebitRepairContainer from './directdebit/containers/DirectDebitRepairContainer';
import DirectDebitEditContainer from './directdebit/containers/DirectDebitEditContainer';
import DirectDebitInitiateContainer from './directdebit/containers/DirectDebitInitiateContainer';
import RTPInitiateContainer from './RTP/Containers/RTPContainer';
import DirectDebitConfirmation from './directdebit/DirectDebitConfirmation';
import DirectDebitInstructionInitiateContainer from './directdebit/DirectDebitInstruction/containers/DirectDebitInstructionInitiateContainer';
import DirectDebitInstructionEditContainer from './directdebit/DirectDebitInstruction/containers/DirectDebitInstructionEditContainer';
import DirectDebitInstructionRepairContainer from './directdebit/DirectDebitInstruction/containers/DirectDebitInstructionRepairContainer';
import { getUserDetails } from '../login/reducer';
import DDATransactionPage from './lists/managelists/MandateTransactionList';
import MandateSummaryBatch from './lists/summarybatch/MandateSummaryBatch';
import DDISummaryBatch from './lists/summarybatch/DDISummaryBatch';
import MandateInitiateContainer from './mandate/containers/MandateInitiateContainer';
import MandateInstructionInitationContainer from './mandate/containers/MandateInstructionInitationContainer';
import MandateConfirmationPage from './mandate/MandateBatch/MandateConfirmation';
import DirectDebitBatchPage from './lists/managelists/DirectDebitBatchList';
import DDITransactionView from './lists/transactiondetailsview/DDITransactionView';
import MandateTransactionView from './lists/transactiondetailsview/MandateTransactionView';
import FilesPage from './lists/managelists/FilesList';
import DDABatchesPage from '../collections/lists/managelists/MandateBatchList';
import DDITransactionsPage from './lists/managelists/DirectDebitTransactionList';
import ApproveMandateList from '../collections/lists/approvelist/MandateList';
import AmandmentMandate from '../collections/lists/approvelist/AmandmentMandate';
import ApproveMandatePage from './Approve/ApproveMandate';
import ApproveDDIList from '../collections/lists/approvelist/DirectDebitBatchList';
import ApproveDDIPage from './Approve/ApproveDDI';
import {
  bulkImportBasePath,
  universalAdapterCreate,
  universalAdapterEdit,
  universalAdapterCopy
} from '../common/CommonRoutes';
import Import from '../common/bulkimport/Import';
import FileSummary from './lists/filesummary/FileSummary';
import PayerInitiatedMandate from './lists/approvelist/PayerInitiatedMandate';
import MandateEditContainer from './mandate/containers/MandateEditContainer';
import MandateReapirContainer from './mandate/containers/MandateRepairContainer';

import MandateInstructionEditContainer from './mandate/containers/MandateInstructionEditContainer';
import MandateInstructionAmendContainer from './mandate/containers/MandateInstructionAmendContainer';
debugger;
export const collectionBasePath = process.env.REACT_APP_COLLECTIONS_BASE_PATH;
const actions = [
  {
    id: 'udaCreateTemplate',
    label: 'CREATE NEW UDA TEMPLATE',
    action: `/${universalAdapterCreate}/template`
  },
  {
    id: 'udaEditTemplate',
    label: 'EDIT UDA TEMPLATE',
    action: `/${universalAdapterEdit}/template`
  },
  {
    id: 'udaCopyTemplate',
    label: 'COPY UDA TEMPLATE',
    action: `/${universalAdapterCopy}/template`
  },
  {
    id: 'directdebit',
    label: 'CREATE NEW DIRECT DEBIT',
    action: `/${collectionBasePath}/directdebit/initiate`
  },
  {
    id: 'MANDATE',
    label: 'CREATE NEW MANDATE',
    action: `/${collectionBasePath}/mandate/initiate`
  },
  {
    id: 'MANAGE',
    label: 'MANAGE LIST',
    action: `/${collectionBasePath}/lists/managelists/mandate/batches`
  },
  {
    id: 'APPROVE',
    label: 'APPROVE LIST',
    action: `/${collectionBasePath}/lists/approvelist/ddi/batches`
  },
  {
    id: 'BULKIMPORT',
    label: 'UPLOAD A DDI FILE',
    action: `/${bulkImportBasePath}/bulkimport/import/ddi`
  },
  {
    id: 'BULKIMPORT',
    label: 'UPLOAD A DDA FILE',
    action: `/${bulkImportBasePath}/bulkimport/import/mandate`
  },
  {
    id: 'BULKIMPORT',
    label: 'UPLOAD A PAYMENT FILE',
    action: `/${bulkImportBasePath}/bulkimport/import/payment`
  },
  {
    id: 'PAYMENTFX',
    label: 'MANAGE FX',
    action: '/payments/lists/managelists/fx'
  }
];

export const MenuRender = (props) => (
  <div>
    {props.userDetails && props.userDetails.userName ? (
      <S2BMenu
        showMenu
        showPopUp
        headerDetails={props.userDetails}
        actions={actions}
      />
    ) : (
      <S2BMenu showMenu={false} actions={actions} />
    )}
  </div>
);

// Declare all the Collections Route here
export const CollectionsRoutes = [
  <Route exact path="/login" component={LoginPage} key="/login" />,
  <Route
    path={`/${collectionBasePath}/directdebit/confirmation`}
    component={DirectDebitConfirmation}
    exact
    key={`/${collectionBasePath}/directdebit/confirmation`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/initiate/newddi`}
    component={DirectDebitInstructionInitiateContainer}
    key={`/${collectionBasePath}/directdebit/initiate/newddi`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/initiate/editddi`}
    component={DirectDebitInstructionEditContainer}
    key={`/${collectionBasePath}/directdebit/initiate/editddi`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/initiate/repairddi`}
    component={DirectDebitInstructionRepairContainer}
    key={`/${collectionBasePath}/directdebit/initiate/repairddi`}
  />,
  <Route
    exact
    path={`/${collectionBasePath}/directdebit/initiate`}
    component={DirectDebitInitiateContainer}
    key={`/${collectionBasePath}/directdebit/initiate`}
  />,
  <Route
    exact
    path={`/${collectionBasePath}/rtp/initiate`}
    component={RTPInitiateContainer}
    key={`/${collectionBasePath}/rtp/initiate`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/edit`}
    component={DirectDebitEditContainer}
    exact
    key={`/${collectionBasePath}/directdebit/edit`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/repair`}
    component={DirectDebitRepairContainer}
    exact
    key={`/${collectionBasePath}/directdebit/repair`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit`}
    component={DirectDebitPage}
    exact
    key={`/${collectionBasePath}/directdebit`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/managelists/mandate/transactions`}
    component={DDATransactionPage}
    key={`/${collectionBasePath}/lists/managelists/mandate/transactions`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/managelists/mandate/batches`}
    component={DDABatchesPage}
    key={`/${collectionBasePath}/lists/managelists/mandate/batches`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/managelists/ddi/batches`}
    component={DirectDebitBatchPage}
    key={`/${collectionBasePath}/lists/managelists/ddi/batches`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/managelists/ddi/transactions`}
    component={DDITransactionsPage}
    key={`/${collectionBasePath}/lists/managelists/ddi/transactions`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/batch/batchdetails`}
    component={MandateSummaryBatch}
    key={`/${collectionBasePath}/mandate/batch/batchdetails`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/batch/batchdetails`}
    component={DDISummaryBatch}
    key={`/${collectionBasePath}/directdebit/batch/batchdetails`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/initiate`}
    component={MandateInitiateContainer}
    exact
    key={`/${collectionBasePath}/mandate/initiate`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/initiate/instruction`}
    component={MandateInstructionInitationContainer}
    exact
    key={`/${collectionBasePath}/mandate/initiate/instruction`}
  />,
  <Route
    path={`/${collectionBasePath}/mandateconfirmation`}
    component={MandateConfirmationPage}
    key={`/${collectionBasePath}/mandateconfirmation`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/transaction/transactionDetails`}
    component={MandateTransactionView}
    exact
    key={`/${collectionBasePath}/mandate/transaction/transactionDetails`}
  />,
  <Route
    path={`/${collectionBasePath}/directdebit/transaction/transactionDetails`}
    component={DDITransactionView}
    exact
    key={`/${collectionBasePath}/directdebit/transaction/transactionDetails`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/managelists/files`}
    component={FilesPage}
    key={`/${collectionBasePath}/lists/managelists/files`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/approvelist/mandate/batches`}
    component={ApproveMandateList}
    exact
    key={`/${collectionBasePath}/lists/approvelist/mandate/batches`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/approvelist/mandate/amendment`}
    component={AmandmentMandate}
    key={`/${collectionBasePath}/lists/approvelist/mandate/amendment`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/batch/signing`}
    component={ApproveMandatePage}
    exact
    key={`/${collectionBasePath}/mandate/batch/signing`}
  />,
  <Route
    path={`/${bulkImportBasePath}/import`}
    component={Import}
    key={`/${bulkImportBasePath}/import`}
  />,
  <Route
    path={`/${collectionBasePath}/file/filesummary`}
    component={FileSummary}
    key={`/${collectionBasePath}/file/filesummary`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/approvelist/ddi/batches`}
    component={ApproveDDIList}
    key={`/${collectionBasePath}/lists/approvelist/ddi/batches`}
  />,
  <Route
    path={`/${collectionBasePath}/ddi/batch/signing`}
    component={ApproveDDIPage}
    key={`/${collectionBasePath}/ddi/batch/signing`}
  />,
  <Route
    path={`/${collectionBasePath}/lists/approvelist/mandate/payerinitiated`}
    component={PayerInitiatedMandate}
    key={`/${collectionBasePath}/lists/approvelist/mandate/payerinitiated`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/amend/instruction`}
    component={MandateInstructionAmendContainer}
    exact
    key={`/${collectionBasePath}/mandate/amend/instruction`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/edit/instruction`}
    component={MandateInstructionEditContainer}
    exact
    key={`/${collectionBasePath}/mandate/edit/instruction`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/repair/instruction`}
    render={(props) => (
      <MandateInstructionEditContainer {...props} isRepairMode />
    )}
    exact
    key={`/${collectionBasePath}/mandate/repair/instruction`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/edit`}
    component={MandateEditContainer}
    exact
    key={`/${collectionBasePath}/mandate/edit`}
  />,
  <Route
    path={`/${collectionBasePath}/mandate/repair`}
    component={MandateReapirContainer}
    exact
    key={`/${collectionBasePath}/mandate/repair`}
  />
];

function mapStateToProps(state) {
  return {
    userDetails: getUserDetails(state)
  };
}
MenuRender.propTypes = {
  userDetails: PropTypes.any
};
export default connect(mapStateToProps)(MenuRender);
